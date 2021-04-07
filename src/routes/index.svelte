<script>
  import { onMount } from "svelte";

  let L;
  let markers = [];
  let blackIcon;

  onMount(async () => {
    L = await import("leaflet");
    mapAction(mapContainer);
    blackIcon = new L.Icon({
      iconUrl:
        "https://raw.githubusercontent.com/pointhi/leaflet-color-markers/master/img/marker-icon-black.png",
      shadowUrl:
        "https://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.7/images/marker-shadow.png",
      iconSize: [25, 41],
      iconAnchor: [12, 41],
      popupAnchor: [1, -34],
      shadowSize: [41, 41],
    });
    let marks = [
      [-37.8142176, 144.9631608],
      [-37.8142176, 145.1631608],
      [-37.8142176, 145.31631608],
    ];

    createMarkers(marks, map);
  });

  // If you're playing with this in the Svelte REPL, import the CSS using the
  // syntax in svelte:head instead. For normal development, this is better.
  import "leaflet/dist/leaflet.css";
  let map;

  function createMarkers(markers, map) {
    markers.forEach((m) => {
      L.marker(m, { icon: blackIcon }).addTo(map);
    });
  }

  function createMap(container) {
    let m = L.map(container).setView([-37.8142176, 144.9631608], 10);
    L.tileLayer(
      "https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}{r}.png",
      {
        attribution: `&copy;<a href="https://www.openstreetmap.org/copyright" target="_blank">OpenStreetMap</a>,
          &copy;<a href="https://carto.com/attributions" target="_blank">CARTO</a>`,
        subdomains: "abcd",
        maxZoom: 21,
      }
    ).addTo(m);

    return m;
  }

  function mapAction(container) {
    map = createMap(container);
    return {
      destroy: () => {
        map.remove();
      },
    };
  }

  let mapContainer;
</script>

<svelte:head>
  <!-- In the REPL you need to do this. In a normal Svelte app, use a CSS Rollup plugin and import it from the leaflet package. -->
  <link
    rel="stylesheet"
    href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css"
    integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
    crossorigin=""
  />
</svelte:head>

<div bind:this={mapContainer} style="height:100vh;width:100%" />

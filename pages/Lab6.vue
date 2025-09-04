<template>
  <div style="height:100vh; width:100vw">
    <LMap
        :zoom="11"
        :center ="petropavl"
        :use-global-leaflet="false">
      style = "height:100%; width:100%;"
      >
      <LTileLayer
          url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
          attribution="&copy; OpenStreetMap contributors"
      />
      <LMarker :lat-lng="petropavl" :draggable="false">
        <LTooltip permanent direction = "top">Петропавловск (СКО)   </LTooltip>
        <LPopup>Петропавлоск, Северо-Казахстанская область</LPopup>
      </LMarker>

      <LMarker
          v-for="(lake, i) in lakes"
          :key="i"
          :lat-lng="[lake.lat, lake.lng]"
          :draggable="false"
      >
        <LTooltip permanent direction="top"> {{lake.name}} </LTooltip>
        <LPopup>
          <strong>{{lake.name}}</strong><br />
          Электропроводность: {{lake.level}}
        </LPopup>


      </LMarker>

    </LMap>
  </div>
</template>

<script setup lang ="ts">
import {ref} from 'vue'
import { LMap, LTileLayer, LMarker, LTooltip, LPopup} from '@vue-leaflet/vue-leaflet'
import 'leaflet/dist/leaflet.css'

type LatLngTuple = [number, number]

interface Lake {
  name: string
  lat: number
  lng: number
  level:number
}


const petropavl = ref<LatLngTuple>([54.88, 69.16])


const lakes = ref<Lake[]>([

{ name: '0зeро Пëстрое', lat: 54.836699, lng: 69.111328, level:1055 },
{ name: '0зeро белое', lat: 54.927154, lng: 69.254322, level:1200 },
{ name: 'Oзepо горькое', lat: 54.947573, lng: 68.951122, level:1106 },
{ name: '0зeро Поганка', lat: 54.921205, lng: 69.053476, level:1235},
{ name: 'Озеро Дикое',lat: 54.840156, lng: 69.131957, level:1420},
  {name: 'Озеро ГУсиное', lat: 54.79316, lng: 69.13508, level:1320},
])
</script>
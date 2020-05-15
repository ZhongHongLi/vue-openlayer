<template>
 <div class="map_main">
   <Init-Map></Init-Map>
 </div>
</template>

<script>
import 'ol/ol.css';
import Map from 'ol/Map';
import View from 'ol/View';
import {Draw, Modify, Snap} from 'ol/interaction';
import {Tile as TileLayer, Vector as VectorLayer} from 'ol/layer';
import {OSM, Vector as VectorSource} from 'ol/source';
import {Circle as CircleStyle, Fill, Stroke, Style} from 'ol/style';

import InitMap from './initMap'

export default {
 data() {
 return {
 }
 },
 created(){
 },
 components:{
 InitMap
 },
 methods: {
 }
}
</script>

<style lang="less" scoped>
#map{
    width: 100vw;
    height: 100vh;
}
</style>

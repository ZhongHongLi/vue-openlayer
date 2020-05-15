<template>
 <div id="map">
 <form class="form-inline">
      <label>Geometry type &nbsp;</label>
      <select id="type"  v-model="ProductActive"  @change="changeProduct($event)">
        <!-- <option value="Point"  ref="pion">Point</option>
        <option value="LineString">LineString</option>
        <option value="Polygon">Polygon</option>
        <option value="Circle">Circle</option> -->
        <option :value="item.target"  v-for="(item,index) in optiondata" :key="index">{{item.target}}</option>
      </select>
    </form>
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

export default {
 data() {
 return {
 map:null,
 ProductActive:'Point',
 optiondata:[
     {id:1,value:'点',target:'Point'},
      {id:2,value:'线',target:'LineString'},
       {id:3,value:'圆',target:'Polygon'},
        {id:4,value:'多边形',target:'Circle'}
 ]
 }
 },
 mounted(){
this.initMap()
 },
 methods: {
     changeProduct(e){
   console.log(e.target.value)
   var  changetarget=e.target.value
//    this.initMap(changetarget)
     },
 initMap(){
 var raster = new TileLayer({
  source: new OSM()
});
var source = new VectorSource();
var vector = new VectorLayer({
  source: source,
  style: new Style({
    fill: new Fill({
      color: 'rgba(255, 255, 255, 0.2)'
    }),
    stroke: new Stroke({
      color: '#ffcc33',
      width: 2
    }),
    image: new CircleStyle({
      radius: 7,
      fill: new Fill({
        color: '#ffcc33'
      })
    })
  })
});

var map = new Map({
  layers: [raster, vector],
  target: 'map',
  view: new View({
    center: [-11000000, 4600000],
    zoom: 4
  })
});
var modify = new Modify({source: source});
map.addInteraction(modify);

var draw, snap; // global so we can remove them later
var typeSelect = document.getElementById('type');
// window.addEventListener('onchange',a)
// console.log(changetarget)


function addInteractions() {
  draw = new Draw({
    source: source,
    type: typeSelect.value
  });
  map.addInteraction(draw);
  snap = new Snap({source: source});
  map.addInteraction(snap);

}
// console.log(typeSelect.onchange)
typeSelect.onchange = function() {
  map.removeInteraction(draw);
  map.removeInteraction(snap);
  addInteractions();
};

addInteractions();

map.on('click',function(e){
    //坐标
    console.log(e.coordinate)
})

 } 
 }
}
</script>

<style lang="less" scoped>
#map{
    width: 100vw;
    height: 100vh;
    z-index: 100;
}
</style>

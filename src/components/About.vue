<template>
    <v-container fluid :style="{color: $store.getters.current.textColor}">
        <v-container fluid
                     :style="{backgroundColor: $store.getters.current.secondary + $store.getters.alpha}">
            <h1 class="pl-1">Info</h1>
        </v-container>
        <v-container fluid class="mt-3"
                     :style="{backgroundColor: $store.getters.current.secondary + $store.getters.alpha}">
            <div v-for="(stat, index) in infoList" :key="index" style="width: 50%">
                <h3>{{stat.name}}</h3>
                <v-row dense>
                    <v-col><p>{{stat.shortValue}}</p></v-col>
                    <v-col v-if="stat.longValue"><p>{{stat.longValue + (stat.unitLabel ? ' ' + stat.unitLabel :
                        '')}}</p>
                    </v-col>
                </v-row>
            </div>
        </v-container>
    </v-container>
</template>

<script>
    import store from '../store/index'
    import {dataUnits, numberUnits, formatNumber} from "@/constants";

    export default {
        name: "About",
        data() {
            return {
                rel: 0,
                infoList: [{
                    name: 'Client Version (Temporary fake data)',
                    shortValue: '1.0.0',
                    longValue: 'latest: x.x.x'
                }, {
                    name: 'Total Hits',
                    unitLabel: 'hits',
                    longValue: store.getters.lastValueOf('hits'),
                    shortValue: formatNumber(store.getters.lastValueOf('hits'), numberUnits),
                }, {
                    name: 'Total Misses',
                    unitLabel: 'misses',
                    longValue:  store.getters.lastValueOf('misses'),
                    shortValue: formatNumber(store.getters.lastValueOf('misses'), numberUnits),
                }, {
                    name: 'Total Data Sent',
                    unitLabel: 'bytes',
                    longValue: store.getters.lastValueOf('bytesSent'),
                    shortValue: formatNumber(store.getters.lastValueOf('bytesSent'), dataUnits),
                }, {
                    name: 'Total Requests Served',
                    unitLabel: 'requests',
                    longValue: store.getters.lastValueOf('reqServ'),
                    shortValue: formatNumber(store.getters.lastValueOf('reqServ'), numberUnits),
                }, {
                    name: 'Cache Size',
                    unitLabel: 'bytes',
                    longValue: store.getters.lastValueOf('sizeDisk'),
                    shortValue: formatNumber(store.getters.lastValueOf('sizeDisk'), dataUnits),
                }],
            }
        },
    }
</script>

<style scoped>

</style>
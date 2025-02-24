<script setup>
import { ref, computed } from "vue";
import LocalVueUiWaffle from '../src/components/vue-ui-waffle.vue';
import LocalVueDataUi from '../src/components/vue-data-ui.vue';
import Box from "./Box.vue";
import convertArrayToObject from "./convertModel";
import { useArena } from "../src/useArena";

const { local, build, vduiLocal, vduiBuild, toggleTable } = useArena()

const dataset = ref([
    {
        name: 'Lorem Ipsum',
        values: [100.27]
    },
    {
        name: 'Dolor Amet',
        values: [66.3367]
    },
    {
        name: 'Dignissimos Ducimus',
        values: [44.25]
    }
]);

const model = ref([
    { key: 'responsive', def: false, type: 'checkbox'},
    { key: 'userOptions.show', def: true, type: 'checkbox'},
    { key: 'userOptions.buttons.pdf', def: true, type: 'checkbox'},
    { key: 'userOptions.buttons.img', def: true, type: 'checkbox'},
    { key: 'userOptions.buttons.table', def: true, type: 'checkbox'},
    { key: 'userOptions.buttons.csv', def: true, type: 'checkbox'},
    { key: 'userOptions.buttons.fullscreen', def: true, type: 'checkbox'},
    { key: 'useBlurOnHover', def: true, type: 'checkbox'},
    { key: 'useCustomCells', def: false, type: 'checkbox'},
    { key: 'useAnimation', def: true, type: 'checkbox'},
    { key: 'style.fontFamily', def: "inherit", type: 'text'},
    { key: 'style.chart.backgroundColor', def: '#FFFFFF', type: 'color'},
    { key: 'style.chart.color', def: '#1A1A1A', type: 'color'},
    { key: 'style.chart.layout.labels.dataLabels.prefix', def: '$', type: 'text'},
    { key: 'style.chart.layout.labels.dataLabels.suffix', def: '€', type: 'text'},
    { key: 'style.chart.layout.labels.captions.show', def: true, type: 'checkbox'},
    { key: 'style.chart.layout.labels.captions.showSerieName', def: true, type: 'checkbox'},
    { key: 'style.chart.layout.labels.captions.serieNameAbbreviation', def: true, type: 'checkbox'},
    { key: 'style.chart.layout.labels.captions.serieNameMaxAbbreviationSize', def: 3, type: 'number', min: 0, max: 12},
    { key: 'style.chart.layout.labels.captions.fontSize', def: 12, type: 'range', min: 8, max: 48},
    { key: 'style.chart.layout.labels.captions.showValue', def: true, type: 'checkbox'},
    { key: 'style.chart.layout.labels.captions.showPercentage', def: true, type: 'checkbox'},
    { key: 'style.chart.layout.labels.captions.roundingValue', def: 2, type: 'range', min: 0, max: 12},
    { key: 'style.chart.layout.labels.captions.roundingPercentage', def: 2, type: 'range', min: 0, max: 12},
    { key: 'style.chart.layout.labels.captions.offsetX', def: 0, type: 'number', min: -100, max: 100},
    { key: 'style.chart.layout.labels.captions.offsetY', def: 0, type: 'number', min: -100, max: 100},
    { key: 'style.chart.layout.grid.size', def: 10, type: 'range', min: 2, max: 20},
    { key: 'style.chart.layout.grid.spaceBetween', def: 0, type: 'number', min: 0, max: 20},
    { key: 'style.chart.layout.grid.vertical', def: false, type: 'checkbox'},
    { key: 'style.chart.layout.rect.rounded', def: true, type: 'checkbox'},
    { key: 'style.chart.layout.rect.rounding', def: 2, type: 'number', min: 0, max: 100},
    { key: 'style.chart.layout.rect.stroke', def: '#1A1A1A', type: 'text'},
    { key: 'style.chart.layout.rect.strokeWidth', def: 1, type: 'number', min: 0, max: 12},
    { key: 'style.chart.layout.rect.useGradient', def: true, type: 'checkbox'},
    { key: 'style.chart.layout.rect.gradientIntensity', def: 40, type: 'range', min: 0, max: 100},
    { key: 'style.chart.title.text', def: 'At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiis', type: 'text'},
    { key: 'style.chart.title.color', def: '#1A1A1A', type: 'color'},
    { key: 'style.chart.title.fontSize', def: 20, type: 'number', min: 8, max: 48},
    { key: 'style.chart.title.bold', def: true, type: 'checkbox'},
    { key: 'style.chart.title.subtitle.text', def: 'At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiis', type: 'text'},
    { key: 'style.chart.title.subtitle.color', def: '#CCCCCC', type: 'color'},
    { key: 'style.chart.title.subtitle.fontSize', def: 16, type: 'range', min: 8, max: 48},
    { key: 'style.chart.title.subtitle.bold', def: false, type: 'checkbox'},
    { key: 'style.chart.tooltip.show', def: true, type: 'checkbox'},
    { key: 'style.chart.tooltip.backgroundColor', def: '#FFFFFF', type: 'color'},
    { key: 'style.chart.tooltip.color', def: '#1A1A1A', type: 'color'},
    { key: 'style.chart.tooltip.fontSize', def: 12, type: 'range', min: 8, max: 48},
    { key: 'style.chart.tooltip.showValue', def: true, type: 'checkbox'},
    { key: 'style.chart.tooltip.showPercentage', def: true, type: 'checkbox'},
    { key: 'style.chart.tooltip.roundingValue', def: 0, type: 'range', min: 0, max: 12},
    { key: 'style.chart.tooltip.roundingPercentage', def: 0, type: 'range', min: 0, max: 12},
    { key: 'table.show', def: false, type: 'checkbox'},
    { key: 'table.responsiveBreakpoint', def: 400, type: 'number', min: 300, max: 800},
    { key: 'table.columnNames.series', def: 'Series', type: 'text' },
    { key: 'table.columnNames.value', def: 'Value', type: 'text' },
    { key: 'table.columnNames.percentage', def: 'Percentage', type: 'text' },
    { key: 'table.th.backgroundColor', def: '#FFFFFF', type: 'color'},
    { key: 'table.th.color', def: '#1A1A1A', type: 'color'},
    { key: 'table.th.outline', def: 'none', type: 'text'},
    { key: 'table.td.backgroundColor', def: '#FFFFFF', type: 'color'},
    { key: 'table.td.color', def: ' #1A1A1A', type: 'color'},
    { key: 'table.td.outline', def: 'none', type: 'text'},
    { key: 'table.td.roundingValue', def: 0, type: 'range', min: 0, max: 12},
    { key: 'table.td.roundingPercentage', def: 0, type: 'range', min: 0, max: 12},
])

const testCustomTooltip = ref(false);

const themeOptions = ref([
    "hack",
    "zen",
    "concrete",
    "default"
])

const currentTheme = ref(themeOptions.value[3])

const config = computed(() => {
    const c = convertArrayToObject(model.value);
    if(testCustomTooltip.value) {
        return {
            ...c,
            style: {
                ...c.style,
                chart: {
                    ...c.style.chart,
                    tooltip: {
                        ...c.style.chart.tooltip,
                        customFormat: ({ datapoint }) => {
                            let html = '';
                            console.log(datapoint);
                            return "test"
                        }
                    }
                }
            }

        }
    } else {
        return {
            ...c,
            theme: currentTheme.value,
            customPalette: ['#6376DD', "#DD3322", "#66DDAA"],
        }
    }
});

const step = ref(0)

function selectLegend(legend) {
    console.log({legend})
}
</script>

<template>
    <button @click="toggleTable">TOGGLE TABLE</button>
    <div style="margin: 12px 0; color: white">
        Theme:
        <select v-model="currentTheme" @change="step += 1">
            <option v-for="opt in themeOptions">{{ opt }}</option>
        </select>
    </div>
    <div style="margin: 12px 0">
        <input type="checkbox" v-model="testCustomTooltip" id="custom-tooltip" />
        <label for="custom-tooltip" style="color:#CCCCCC">Test custom tooltip</label>
    </div>

    <div style="width: 600px; height: 600px; resize: both; overflow: auto; background: white">
        <LocalVueUiWaffle :key="`responsive_${step}`" :dataset="dataset" :config="{
            ...config,
            responsive: true
        }"/>
    </div>

    <Box comp="VueUiWaffle" :dataset="dataset">
        <template #title>VueUiWaffle</template>

        <template #local>
            <LocalVueUiWaffle :dataset="dataset" :config="config" :key="`local_${step}`" @selectLegend="selectLegend" ref="local">
                <template #optionPdf>
                    PRINT PDF
                </template>
                <template #cell="{ cell, isSelected }">
                    <div :style="`opacity:${isSelected ? 1 : 0.3}`">
                        <VueUiIcon
                            v-if="cell.name === 'Lorem Ipsum'"
                            name="lambda"
                            size="40"
                            :stroke="cell.color"
                        />
                        <VueUiIcon
                            v-if="cell.name === 'Dolor Amet'"
                            name="func"
                            size="40"
                            :stroke="cell.color"
                        />
                        <VueUiIcon
                            v-if="cell.name === 'Dignissimos Ducimus'"
                            name="mu"
                            size="40"
                            :stroke="cell.color"
                        />
                    </div>
                </template>
                <template #svg="{ svg }">
                    <circle :cx="svg.width / 2" :cy="svg.height / 2" :r="30" fill="#42d392" />
                    <text :x="svg.width / 2" :y="svg.height / 2" text-anchor="middle">#SVG</text>
                </template>
                <template #legend="{ legend }">
                    #LEGEND
                    <div style="font-size: 8px">
                        {{ legend }}
                    </div>
                </template>
                <template #tooltip-before="{ datapoint, seriesIndex, series, config, bars, lines, plots }">
                    #BEFORE {{ series.name }}
                </template>
                <template #tooltip-after="{ datapoint, seriesIndex, series, config, bars, lines, plots }">
                    #AFTER {{ series.name }}
                </template>
            </LocalVueUiWaffle>
        </template>

        <template #VDUI-local>
            <LocalVueDataUi component="VueUiWaffle" :dataset="dataset" :config="config" :key="`VDUI-lodal_${step}`" @selectLegend="selectLegend" ref="vduiLocal">
                <template #cell="{ cell, isSelected }">
                    <div :style="`opacity:${isSelected ? 1 : 0.3}`">
                        <VueUiIcon
                            v-if="cell.name === 'Lorem Ipsum'"
                            name="lambda"
                            :size="40"
                            :stroke="cell.color"
                        />
                        <VueUiIcon
                            v-if="cell.name === 'Dolor Amet'"
                            name="func"
                            :size="40"
                            :stroke="cell.color"
                        />
                        <VueUiIcon
                            v-if="cell.name === 'Dignissimos Ducimus'"
                            name="mu"
                            :size="40"
                            :stroke="cell.color"
                        />
                    </div>
                </template>
                <template #svg="{ svg }">
                    <circle :cx="svg.width / 2" :cy="svg.height / 2" :r="30" fill="#42d392" />
                    <text :x="svg.width / 2" :y="svg.height / 2" text-anchor="middle">#SVG</text>
                </template>
                <template #legend="{ legend }">
                    #LEGEND
                    <div style="font-size: 8px">
                        {{ legend }}
                    </div>
                </template>
                <template #tooltip-before="{ datapoint, seriesIndex, series, config, bars, lines, plots }">
                    #BEFORE {{ series.name }}
                </template>
                <template #tooltip-after="{ datapoint, seriesIndex, series, config, bars, lines, plots }">
                    #AFTER {{ series.name }}
                </template>
            </LocalVueDataUi>
        </template>

        <template #build>
            <VueUiWaffle :dataset="dataset" :config="config" :key="`build_${step}`" @selectLegend="selectLegend" ref="build">
                <template #cell="{ cell, isSelected }">
                    <div :style="`opacity:${isSelected ? 1 : 0.3}`">
                        <VueUiIcon
                            v-if="cell.name === 'Lorem Ipsum'"
                            name="lambda"
                            size="40"
                            :stroke="cell.color"
                        />
                        <VueUiIcon
                            v-if="cell.name === 'Dolor Amet'"
                            name="func"
                            size="40"
                            :stroke="cell.color"
                        />
                        <VueUiIcon
                            v-if="cell.name === 'Dignissimos Ducimus'"
                            name="mu"
                            size="40"
                            :stroke="cell.color"
                        />
                    </div>
                </template>
                <template #svg="{ svg }">
                    <circle :cx="svg.width / 2" :cy="svg.height / 2" :r="30" fill="#42d392" />
                    <text :x="svg.width / 2" :y="svg.height / 2" text-anchor="middle">#SVG</text>
                </template>
                <template #legend="{ legend }">
                    #LEGEND
                    <div style="font-size: 8px">
                        {{ legend }}
                    </div>
                </template>
                <template #tooltip-before="{ datapoint, seriesIndex, series, config, bars, lines, plots }">
                    #BEFORE {{ series.name }}
                </template>
                <template #tooltip-after="{ datapoint, seriesIndex, series, config, bars, lines, plots }">
                    #AFTER {{ series.name }}
                </template>
            </VueUiWaffle>
        </template>

        <template #VDUI-build>
            <VueDataUi component="VueUiWaffle" :dataset="dataset" :config="config" :key="`VDUI-build_${step}`" @selectLegend="selectLegend" ref="vduiBuild">
                <template #cell="{ cell, isSelected }">
                    <div :style="`opacity:${isSelected ? 1 : 0.3}`">
                        <VueUiIcon
                            v-if="cell.name === 'Lorem Ipsum'"
                            name="lambda"
                            size="40"
                            :stroke="cell.color"
                        />
                        <VueUiIcon
                            v-if="cell.name === 'Dolor Amet'"
                            name="func"
                            size="40"
                            :stroke="cell.color"
                        />
                        <VueUiIcon
                            v-if="cell.name === 'Dignissimos Ducimus'"
                            name="mu"
                            size="40"
                            :stroke="cell.color"
                        />
                    </div>
                </template>
                <template #svg="{ svg }">
                    <circle :cx="svg.width / 2" :cy="svg.height / 2" :r="30" fill="#42d392" />
                    <text :x="svg.width / 2" :y="svg.height / 2" text-anchor="middle">#SVG</text>
                </template>
                <template #legend="{ legend }">
                    #LEGEND
                    <div style="font-size: 8px">
                        {{ legend }}
                    </div>
                </template>
                <template #tooltip-before="{ datapoint, seriesIndex, series, config, bars, lines, plots }">
                    #BEFORE {{ series.name }}
                </template>
                <template #tooltip-after="{ datapoint, seriesIndex, series, config, bars, lines, plots }">
                    #AFTER {{ series.name }}
                </template>
            </VueDataUi>
        </template>

        <template #knobs>
            <div
                style="display: flex; flex-direction: row; flex-wrap:wrap; align-items:center; width: 100%; color: #CCCCCC; gap:24px;">
                <div v-for="knob in model">
                    <label style="font-size: 10px">{{ knob.key }}</label>
                    <div
                        style="display:flex; flex-direction:row; flex-wrap: wrap; align-items:center; gap:6px; height: 40px">
                        <input v-if="!['none', 'select'].includes(knob.type)" :step="knob.step" :type="knob.type" :min="knob.min ?? 0"
                            :max="knob.max ?? 0" v-model="knob.def" @change="step += 1">
                        <select v-if="knob.type === 'select'" v-model="knob.def" @change="step += 1">
                            <option v-for="opt in knob.options">{{ opt }}</option>
                        </select>
                    </div>
                </div>
            </div>
        </template>

        <template #config>
            {{ config }}
        </template>
    </Box>
</template>
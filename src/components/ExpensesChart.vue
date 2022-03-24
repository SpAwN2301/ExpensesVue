<template>
    <div class="ExpensesChart">
        <DoughnutChart v-bind="doughnutChartProps" />
    </div>
</template>

<script lang='ts'>
import { computed, defineComponent, ref, toRefs } from "vue";
import { DoughnutChart, useDoughnutChart } from "vue-chart-3";
import { Chart, ChartData, ChartOptions, registerables } from "chart.js";

Chart.register(...registerables);
export default defineComponent({
    name: "App",
    components: { DoughnutChart },
    props: {
        names: Array,
        costs: Array,
    },
    setup(props) {
        const { names, costs } = toRefs(props);
        const dataValues = costs;
        const dataLabels = names;
        const toggleLegend = ref(true);

        const testData = computed<ChartData<"doughnut">>(() => ({
            labels: dataLabels.value,
            datasets: [
                {
                    data: dataValues.value,
                    backgroundColor: [
                        "#44B549",
                        "#117ebe",
                        "#ec3536",
                        "#578B9A",
                        "#FFCD27",
                    ],
                },
            ],
        }));

        const options = computed<ChartOptions<"doughnut">>(() => ({
        }));

        const { doughnutChartProps, doughnutChartRef } = useDoughnutChart({
            chartData: testData,
            options,
        });

        let index = ref(20);

        function shuffleData() {
            // dataValues.value = shuffle(dataValues.value);
            dataValues.value.push(index.value);
            dataLabels.value.push("Other" + index.value);
            console.log(dataValues.value);
            console.log(doughnutChartRef.value.chartInstance);
            index.value++;
        }

        function switchLegend() {
            toggleLegend.value = !toggleLegend.value;
        }

        return {
            shuffleData,
            switchLegend,
            testData,
            options,
            doughnutChartRef,
            doughnutChartProps,
        };
    },
});
</script>

<style lang="scss" scoped>
.ExpensesChart {

    @media (min-width: 420px) {
        width: 40vw;
    }
}
</style>

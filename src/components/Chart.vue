<script>
import { Line } from 'vue-chartjs'

export default {
    extends: Line,
    props: ['chartdata'],
    data() {
        return {
            options: {
                scales: {
                    yAxes: [{
                        ticks: {
                            beginAtZero: true
                        }
                    }]
                }
            }
        }
    },
    mounted () {
        this.renderChart(this.chartdata, this.options)
    },
    methods: {
        updateChartDisplay(data){
            this.renderChart(data, this.options);
        }
    }
}
</script>

<style>
</style>

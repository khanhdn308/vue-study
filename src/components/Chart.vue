<script>
import { Line } from 'vue-chartjs'

export default {
    extends: Line,
    props: ['chartdata'],
    mounted () {
        this.renderChart(this.chartdata)
    }
}
</script>

<style>
</style>

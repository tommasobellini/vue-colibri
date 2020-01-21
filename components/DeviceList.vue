<template>
    <view class="container">
        <view class="listContainer">
            <touchable-opacity v-for="device in devices" :key="device.id" underlayColor="#eee" class="listItem" :on-press="onDevicePressed(device)">
                <view style="flexDirection: column;">
                    <view style="flexDirection: row;">
                        <text class="listItemStatus" :style="device.paired ? 'backgroundColor: #4ec5a5' : 'backgroundColor: gray'">
                            {{device.paired ? "PAIRED" : "UNPAIRED"}}
                        </text>
                         <text class="listItemStatus" :style="device.connected ? 'backgroundColor: green' : 'backgroundColor: gray'">
                            {{device.paired ?  "CONNECTED" : "DISCONNECTED"}}
                        </text>
                    </view>
                     <view  style="flexDirection: column;">
                        <text style="fontWeight: bold; fontSize: 18;">
                            {{device.name}}
                        </text>
                        <text>{{`<${device.id}>`}}</text>
                    </view>
                </view>
            </touchable-opacity>
        </view>
    </view>
</template>

<script>
export default {
    name: 'DeviceList',
    props: {devices: Array},
    data() {
        return {
            refreshing: false
        }
    },
    methods: {
         onDevicePressed(device){
            if (typeof this.props.onDevicePressed === "function") {
                 this.props.onDevicePressed(device);
            }
        },
        async onRefresh() {
            if (typeof this.props.onRefresh === "function") {
                this.setState({ refreshing: true });
                await this.props.onRefresh();
                this.setState({ refreshing: false });
            }
        }
    }
}
</script>

<style scoped>

</style>
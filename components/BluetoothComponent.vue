<template>
    <view style="flex: 1; backgroundColor: #4ec5a5;">
        <view v-if="scanning"
            style="flex: 1; alignItems: center; justifyContent: center;">
            <activity-indicator
            style="marginBottom: 15;"
            />
            <button
            textStyle="color: #fff;"
            class="buttonRaised"
            title="Cancel Discovery"
            :onPress="cancelDiscovery"
            />
        </view>
          <view v-else>
            <device-list
              :devices="devices"
              :onRefresh="listDevices"
            />
          </view>
    </view>
</template>

<script>
import DeviceList from "./DeviceList";
import { BleManager } from "react-native-ble-plx"
import Toast from "@remobile/react-native-toast";

export default {
    name: 'BluetoothComponent',
    data() {
        return {
            isEnabled: false,
            device: 3,
            devices: [],
            scanning: false,
            processing: false,
            temporing: 0,
            services: {},
            payload: null,
            vibes: 0
        }
    },
    async created() {
        const manager = new BleManager()
        Toast.showShortTop(JSON.stringify(manager))

        manager.state().then(resp1 => {
        Toast.showShortTop(resp1)
        if (resp1 === 'PoweredOn') {
            this.listDevices().then(list => {
                // console.log(list)
                this.setState(({ devices }) => ({
                devices: devices.map(device => {
                    const found = list.find(v => v.id === device.id);
                    // console.log(found)
                    if (found) {
                    return {
                        ...found,
                        paired: true,
                        connected: false
                    };
                    }
                    // console.log(device)
                    return device;
                })
                }));
                // console.log(this.state.devices)

            })
            
        }
        })
    },
    methods: {
          async toggleDeviceConnection({ id, connected }) {
                if (connected) {
                    await this.disconnect(id);
                } else {
                    await this.connect(id);
                }
            },
            async listDevices() {
                try {
                    const list = await BleManager.list();
                    return list
                } catch (e) {
                    Toast.showShortBottom(e.message);
                }
            },
    },
    components: {DeviceList}
}
</script>

<style scoped>

</style>
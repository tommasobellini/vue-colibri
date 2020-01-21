<template>
    <view style="display: flex;">
         <modal
          :isVisible="modalVisible"
        >
          <touchable-opacity
          >
            <button title="Close" color='#4ec5a5' :onPress="() => {
              setModalVisible(false);
            }" />
          </touchable-opacity>

          <view style="flex: 1; background-color: white;">
            <bluetooth-component/>
          </view>
        </modal>
        <view class="topBar">
          <text class="heading">Dashboard</text>
          <touchable-opacity
            class="plusIcon"
            :onPress="() => {
              setModalVisible(true);
            }"
          >
            <icon name='plus' color="#fff" style="font-size: 25;"/>
          </touchable-opacity>
        </view>
        <view class="cyclesSection">
          <view class="outsideRingCyclesSection" >
            <view class="insideRingsContainerCyclesSection" >
              <view :class="'insideRingCyclesSection'"></view>
              <view  class="insideRingWithOpacityCyclesSection"></view>
              <view :class="'insideRingCyclesSection'"></view>
            </view>
          </view>
        </view>
        <view class="testSection">
          <view class="testContainerSection">
            <touchable-opacity
              class="buttonTestSection"
              :onPress="() => this.startTest()"
            >
              <text>TEST</text>
            </touchable-opacity>
          </view>
        </view>
        <view class="statsSection">
          <view class="stressStatsSection">
            <view class="centerView">
              <image :source="require('../assets/Stress.png')" class="imageStressStatsSection" />
              <text class="textStressStatsSection">Stress : <text style="color: #fbb03b">300</text> </text>
            </view>
            <view>
            </view>
          </view>
          <view class="othersStatsSection">
            <view class="iconsContainer">
                  <view  class="centerIcons" v-for="iconStat in iconsStats" :key="iconStat.id">
                    <image :source="iconStat.path" class="imageIcon" />
                    <text class="centerTextIcon">{{iconStat.name}}: <text>{{iconStat.value}}</text></text>
                  </view>
            </view>
          </view>
        </view>
    </view>
</template>
<script>
import Icon from 'react-native-vector-icons/FontAwesome5';
import Modal from "react-native-modal";
import BluetoothComponent from '../components/BluetoothComponent'
export default {
    name: 'HomeScreen',
    data() {
        return {
            modalVisible: false,
            isEnabled: true,
            isAlreadyMounted: false,
            vibes: 0,
            dataList: [],
            ciao: true,
            dataX: [0],
            dataY: [0],
            dataZ: [0],
            isShowRing: true,
            iconsStats: [
                {id: 1, name: 'vibes', path: require('../assets/Vibes.png'), value: 55},
                {id: 2, name: 'bpm', path: require('../assets/BPM.png'), value: 100},
                {id: 3, name: 'ir', path: require('../assets/IR.png'), value: 10},
            ]
        }
    },
    mounted() {
        this.animationBlinkRings()
    },
    methods: {
        setModalVisible(visible) {
            this.modalVisible = visible;
        },
        animationBlinkRings() {
            setInterval(() => {
                this.isShowRing = !this.isShowRing
            }, 250)
        }
    },
    components: {
        Icon, Modal, BluetoothComponent
    }
}
</script>
<style scoped>
    .topBar {
        height: 90;
        padding: 25;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        background-color: #4ec5a5;
    }
    .heading {
        margin-top: 25;
        color: white;
        font-size: 20;
    }
    .plusIcon {
        margin-top: 25;
    }
    .showRing {
        opacity: 1;
    }
    .hideRing {
        opacity: 0;
    }
    .cyclesSection {
        height: 250;
        padding-left: 120;
        padding-top: 50;
    }
    .outsideRingCyclesSection {
        height: 150;
        width: 150;
        border-color: #4ec5a5;
        opacity: 0.5;
        border-width: 17;
        border-radius: 100;
    }
    .insideRingsContainerCyclesSection {
        display: flex;
        align-content: center;
        justify-content: center;
        flex-direction: row;
    }
    .insideRingCyclesSection {
        margin: 2;
        margin-top: 43;
        height: 25;
        width: 25;
        background-color: #4ec5a5;
        border-radius: 50;
    }
    .insideRingWithOpacityCyclesSection {
        margin: 2;
        margin-top: 43;
        height: 25;
        width: 25;
        background-color: #4ec5a5;
        border-radius: 50;
        opacity: 0.5;
    }
    .testSection {
        height: 70;
    }
    .testContainerSection {
        margin-left: 120;
    }
    .buttonTestSection {
        background-color: white;
        border-color: #4ec5a5;
        border-width: 2;
        width: 150;
        height: 50;
        padding-left: 60;
        padding-top: 15;
    }
    .statsSection {
        height: 350;
        padding-left: 50;
    }
    .stressStatsSection {
        width: 300;
        height: 100;
        border-color: lightgrey;
        border-width: 1;
        border-top-right-radius: 16;
        border-top-left-radius: 16;
    }
    .imageStressStatsSection {
        width: 70;
        height: 70;
        margin-top: 10;
    }
    .textStressStatsSection {
        text-transform: uppercase;
        margin-left: 10;
        margin-top: 7;
        font-weight: bold;
        /* font-size: 25; */
    }
    .othersStatsSection {
        width: 300;
        height: 200;
        border-color: lightgrey;
        background-color: #DCDCDC;
        border-width: 1;
        border-bottom-right-radius: 16;
        border-bottom-left-radius: 16;
    }
    .centerView {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
    }
    .iconsContainer {
        padding-top: 15;
        font-weight: bold;
        opacity: 1;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
    }
    .centerIcons{
        display: flex;
        flex-direction: row;
        align-content: center;
        justify-content: center;
        margin-left: 75 ;
    }
    .imageIcon {
        width: 35;
        height: 35;
        margin: 5;
    }
    .centerTextIcon {
        font-weight: bold;
        margin-top: 15;
        margin-left: 7;
    }
</style>
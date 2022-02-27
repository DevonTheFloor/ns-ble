<template>
    <Page>
        <ActionBar tile="Bluetooth">
            <Label text="Testing Bluetooth"/>
        </ActionBar>

        <StackLayout class="stac-lay">
            <Label text="Here all the function for use bluetooth" class="h3"/>
            <Label :text="bleMessage" />
            <Button text="Click for BLE" @tap="isBleEnable"/>
            <Button text="Scan Permission" @tap="scanPermission"/>
            <Button text="Turn On" @tap="turnOn"/>
            <Button text="Start Scanning" @tap="startScan"/>
        </StackLayout>
    </Page>
</template>

<script>
import { Bluetooth } from '@nativescript-community/ble'

  export default {
    data () {
        return {
            ble: null,
            bleMessage: null
        }
    },
    computed: {

    },
    mounted() {
    },
    methods: {
        /**
         * Testing the bluetooth connection
         */
        isBleEnable() {
            this.ble = new Bluetooth()
            this.ble.isBluetoothEnabled()
            .then(
                function(enabled) {
                    console.log("Enabled? " + enabled);
                    this.bleMessage = `BLE enable: ${enabled}`
                    return this.bleMessage
                }
            )
        },
        scanPermission() {
            this.ble = new Bluetooth()
            this.ble.hasCoarseLocationPermission()
            .then(function(granted) {
                // if this is 'false' you probably want to call 'requestLocationPermission' now
                console.log("Has Location Permission? " + granted);
                });
        },
        /**
         * Turn on and use bluetooth, ask for permission so
         */
        turnOn () {
            this.ble = new Bluetooth()
            this.ble.enable()
            .then(function(enabled) {
                // use Bluetooth features if enabled is true
                console.log('Turn on :', enabled);
            }
);
        },
        startScan() {
            this.ble = new Bluetooth;
            this.ble.startScanning({
            filters: [{serviceUUID:'180d'}],
            seconds: 4,
            onDiscovered: function (peripheral) {
                console.log("Periperhal found with UUID: " + peripheral.UUID);
                }
            })
            .then(function() {
                console.log("scanning complete");
                }, function (err) {
                    console.log("error while scanning: " + err);
                    });
        }
    }
  };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';

    // Custom styles
    .fas {
        @include colorize($color: accent);
    }

    .info {
        font-size: 20;
        horizontal-align: center;
        vertical-align: center;
    }
    .stac-lay {
         vertical-align: center;
    }
</style>

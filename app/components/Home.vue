<template>
    <Page>
        <ActionBar tile="Bluetooth">
            <Label text="Testing Bluetooth"/>
        </ActionBar>

        <StackLayout class="stac-lay">
            <Label text="Here all the functions for use bluetooth" class="h4" wrap="true"/>
            <Label :text="debugInfo" />
            <Button text="Click for BLE" @tap="isBleEnable"/>
            <Button text="Scan Perm" @tap="scanPermission"/>
            <Button text="Turn On" @tap="turnOn"/>
            <Button text="Start Scanning" @tap="startScan"/>
            <Button text="STOP Scanning" @tap="stopScan"/>
            <Button text="OLD Scanning" @tap="oldScan"/>
        </StackLayout>
    </Page>
</template>

<script>
import { Bluetooth } from '@nativescript-community/ble'
// var bluetooth =require('nativescript-bluetooth') 

  export default {
    data () {
        return {
            ble: new Bluetooth
        }
    },
    computed: {
        debugInfo(message) {
            return message
        }
    },
    mounted() {
    },
    methods: {
        stopScan() {
            this.ble.stopScanning().then(function() {
                message = "Scanning Stopped"
                console.log("scanning stopped");
            });
        },
        oldScan() {
            bluetooth.startScanning({
            serviceUUIDs: [],
            seconds: 4,
            onDiscovered: function (peripheral) {
                console.log("Periperhal found with UUID: " + peripheral.UUID);
            }
            }).then(function() {
            console.log("scanning complete");
            }, function (err) {
            console.log("error while scanning: " + err);
            });
        },
        /**
         * Testing the bluetooth connection
         */
        isBleEnable() {
            this.ble.isBluetoothEnabled()
            .then(
                function(enabled) {
                    console.log("Enabled? " + enabled);
                    this.debugInfo("Coucou en dur")
                }
            )
        },
        /**
         * Don't work
         */
        scanPermission() {
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
            this.ble.enable()
            .then(function(enabled) {
                // use Bluetooth features if enabled is true
                console.log('Turn on :', enabled);
            }
);
        },
        startScan() {
            console.log('Start Scanning...')
            this.ble.startScanning({
            filters: [],
            seconds: 5,
            onDiscovered: function (peripheral) {
                    console.log("Peripheral found with UUID: ", peripheral.UUID);
                }
            })
            .then(function() {
                console.log("scanning completed");
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

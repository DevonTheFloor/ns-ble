<template>
    <Page>
        <ActionBar>
            <Label text="Testing Bluetooth"/>
        </ActionBar>

        <GridLayout>
            <Label class="info">
                <FormattedString>
                    <Span class="fas" text="&#xf135; "/>
                    <Span :text="message"/>
                </FormattedString>
            </Label>
        </GridLayout>
        <StackLayout>
            <Button text="Click to BLE" @tap="isBleEnable"/>
        </StackLayout>
    </Page>
</template>

<script>
import { Bluetooth } from '@nativescript-community/ble'

  export default {
    data () {
        return {
            ble: null
        }
    },
    computed: {
      message() {
        return "Ble enable ok";
      },
    },
    mounted() {
    },
    methods: {
        /**
         * Testing the bluetooth connection
         */
        isBleEnable() {
            this.ble = new Bluetooth();

            this.ble.isBluetoothEnabled()
            .then(
                function(enabled) {
                    console.log("Enabled? " + enabled);
                }
            )
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
</style>

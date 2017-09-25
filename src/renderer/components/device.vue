<template>
    <b-card :no-body="true">
        <div :class="['card-header', isResponsive ? 'bg-primary' : 'bg-danger']">
            <b-dropdown class="float-right" variant="transparent p-0" right>
                <template slot="button-content">
                    <i class="icon-settings"></i>
                </template>
                <b-dropdown-item @click="remove">Remove</b-dropdown-item>
            </b-dropdown>
            <img :src="iconUrl" alt="Device icon" />
        </div>
        <div class="card-body pb-0">
            <h4 class="mb-0">{{ name }}</h4>
            <p>{{ model }}</p>
        </div>
    </b-card>
</template>

<script lang="ts">
import Vue from 'vue';
import 'vuex';
import Component from 'vue-class-component';
import { Device as Model, NetworkStatus } from '../models';
import { REMOVE_DEVICE_MUTATION } from '../store';

@Component({
    name: 'device',
    props: {
        device: {
            type: Model,
            required: true,
        },
    },
})
export default class Device extends Vue {
    private readonly device: Model;

    public get name(): string {
        return this.device.name;
    }

    public get model(): string {
        return this.device.model;
    }

    public get iconUrl(): string {
        return this.device.iconUrl || '';
    }

    public get isResponsive(): boolean {
        return this.device.networkStatus === NetworkStatus.responsive;
    }

    public remove(e: Event) {
        this.$store.commit(REMOVE_DEVICE_MUTATION, this.device);
    }
}
</script>
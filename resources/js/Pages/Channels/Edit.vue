<template>
    <AppLayout title="Channel Create">
        <form @submit.prevent="submit" class="w-full max-w-xl">
            <div class="space-y-12">
                <div class="mb-6">
                    <h2 class="text-base font-semibold leading-7 text-gray-900">Create a new channel</h2>
                    <p class="mt-1 text-sm leading-6 text-gray-600">This information will be used to create your channel.</p>
                </div>
            </div>

            <div class="mb-6">
                <InputLabel for="name" value="Name" />
                <TextInput id="name" v-model="form.name" type="text" required autofocus />
                <InputError class="mt-2" :message="form.errors.name" />
            </div>

            <div class="mb-6">
                <InputLabel for="type" value="Type" />
                <RadioInput id="type" v-model="form.type" :options="[
                    { value: 'whatsapp', label: 'WhatsApp' },
                ]" required />
                <InputError class="mt-2" :message="form.errors.type" />
            </div>

            <div class="flex flex-row text-right">
                <SecondaryButton class="mr-2" :href="route('channels.index')">
                    Cancel
                </SecondaryButton>
                <PrimaryButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Save
                </PrimaryButton>
            </div>
        </form>
    </AppLayout>
</template>

<script setup>
import { useForm } from '@inertiajs/vue3';
import AppLayout from '@/Layouts/AppLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import RadioInput from '@/Components/RadioInput.vue';

const props = defineProps({
    channel: {
        type: Object,
        required: true,
    }
});

const form = useForm({
    name: props.channel.name,
    type: props.channel.type,
});

const submit = () => {
    form.put(route('channels.update', props.channel.id));
};
</script>

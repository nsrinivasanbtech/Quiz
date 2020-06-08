<template>
    <div class="overlay">
        <b-spinner
            class="mx-auto spinnerSize"
            variant="Danger"
        ></b-spinner>
    </div>
</template>

<style>
    .overlay{position: fixed;width: 100%;height: 100%;top: 0;left: 0;right: 0;bottom: 0;background-color: rgba(0,0,0,.5);z-index:2;}
    .spinnerSize{width: 10rem;height:10rem;margin-top: 10%;}
</style>
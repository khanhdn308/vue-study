<template>
    <div class="display-card">
        <img
            class="card-icon"
            :src="imgSource"
            alt="Avatar"
        />
        <div class='card-content'>
            <h3 class='name'>{{ name }}</h3>
            <p>{{ age }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "Card",
    props: {
        name: String,
        imgName: String,
        age: Number,
        imgSource: String
    }
};
</script>

<style>
.display-card {
    background-color: #ffffff;
    border-radius: 5px;
    box-shadow: 0 20px 60px 0 rgba(41, 67, 100, 0.21);
    width: 280px;
    height: 420px;
    padding: 10px;
    text-align: center;
}

.name {
    font-weight: bold;
}

.card-icon {
    pointer-events: none;
    width: 180px;
    padding: 40px 20px 0px 20px;
}

.card-content {
    padding: 20px;
}
</style>
<template>
    <div>
        <b-row>
            <b-col>
                <b-navbar class="navbar">
                    <b-navbar-brand class="mx-auto" href="#"><h1>Quiz</h1></b-navbar-brand>
                    <b-navbar-nav>
                        <b-nav-item href="#" disabled><b>Counter:- {{numCorrect}} / {{numTotal}}</b></b-nav-item>
                    </b-navbar-nav>
                </b-navbar>
            </b-col>
        </b-row>
    </div>
</template>

<script>
    export default {
        props: {
            numCorrect: [String, Number],
            numTotal: [String, Number]
        }
    }
</script>

<style>
    .navbar{background-image: linear-gradient(to right, #f8e2d5 , #7bc5ce);}
    h1{color: #40332b;}
</style>
<template>
<div id="quiz1">
    <div class="com_contain" v-if="step==0">
        <div class="number">Q1 / 5</div>
        <div class="question">
            오랜 역사와 전통을 자랑하는 치즈의 나라인 프랑스에서 오늘날 추산되는 프랑스 치즈의 종류는 <strong>약 몇 가지</strong>일까?
        </div>
        <div class="choice_box">
            <button class="choice" @click="checkAnswer(0)"
            :class="{'check' : isChecked === 0}">
                <i class="pi pi-check"></i>100
            </button>
            <button class="choice" @click="checkAnswer(1)"
            :class="{'check' : isChecked === 1}">
                <i class="pi pi-check"></i>200
            </button>
            <button class="choice" @click="checkAnswer(2)"
            :class="{'check' : isChecked === 2}">
                <i class="pi pi-check"></i>400
            </button>
            <button class="choice" @click="checkAnswer(3)"
            :class="{'check' : isChecked === 3}">
                <i class="pi pi-check"></i>1000 +
            </button>
        </div>
        <button class="mainBtn1" @click="nextQustion()">정답 확인</button>
    </div>

    <div class="com_contain" v-if="step==1">
        <div class="judgement right" v-if="judgement">
            <img src="~public/img/right_check.png" alt="">
            <p>정답이예요!</p>
        </div>
        <div class="judgement wrong" v-else>
            <img src="~public/img/wrong.png" alt="">
            <p>앗, 정답이 아니에요!</p>

        </div>
        <div class="number">정답 확인</div>
        <button class="choice check"><i class="pi pi-check"></i>1000 +</button>
        <div class="explain">
            프랑스는 세계에서 정통 치즈를 <br>
            가장 많이 생산하고, 가장 많이 수출하고, <br>
            가장 많이 먹는 나라로 알려져 있습니다. <br>
            오늘날 추산되는 프랑스 치즈의 종류는 <br>
            <strong>약 1,200개</strong>에 달합니다. <br>
            다채로운 자연환경에서 풍요로운 역사와 <br>
            전통 속에서 만들어지는 프랑스 치즈는 <br>
            전 세계인의 사랑을 받습니다. <br>
            프랑스 외에 이탈리아, 네덜란드, <br>
            스페인 등에서도 치즈를 생산합니다.<br>
        </div>
        <img src="~public/img/quiz/1.jpg" alt="" class="explain_img">
        <button class="mainBtn1" @click="$router.push('/quiz2')">다음 문제<i class="pi pi-arrow-right"></i></button>
    </div>
</div>
</template>

<script setup>
definePageMeta({
    name: "Quiz1Page",
})
const step = ref(0); // 0: 문제, 1: 해설
const isChecked = ref(null); // 문제 보기 체크
const judgement = ref(false); // 문제 맞고 틀리고 판단

const quizStore = useQuizStore();
quizStore.setQuizData(0,false);

const checkAnswer = (no) => {
    isChecked.value = no;
    if(no == 3){
        judgement.value = true;
    }else{
        judgement.value = false;
    }
    quizStore.setQuizData(0,judgement.value);
}
const nextQustion = () => {
    if(isChecked.value == null){
        alert('정답을 선택해주세요');
        return;
    }
    step.value = 1;
}
</script>

<style lang="scss" scoped>
#quiz1{
    .explain_img{
        width: 100%;
        border-radius: $px12;
        margin: 24px 0;
    }
    .choice_box{
        display: flex;
        flex-direction: column;

    }
    .mainBtn1{
        width: 100%;
    }
}

</style>
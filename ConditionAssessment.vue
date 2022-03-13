<template>
    <div class="condition-assessment">
        <div class="test-section">
            <div class="test-header">
                <div id="getStart" class="test-header-text">
                    <span class="head-text">
                        Расскажите, что вас беспокоит  и узнайте, какие исследования  стоит взять с собой на приём к врачу
                    </span>
                     <span class="sub-text">
                        Опрос полностью анонимный, мы не собираем ваши <br> данные. 
                        Просто ответьте на пару вопросов и мы сразу <br> покажем 
                        список необходимых для вас исследований.
                    </span>
                </div>
                <div class="test-header-img">
                    <img class="header-img" src="../assets/test-head-robot.png" alt="">
                </div>
            </div>
            <form class="test-form" action="#">
                <div class="tst-inp">
                    <img class="mini-robot" src="../assets/mini-robot.svg" alt="">
                    <span class="mini-robot-text">Что вы ощущаете?</span>
                </div>
                <input v-model="question_1" class="test-input" type="text" name="" id="txtArea1" placeholder="Например: Боль, усталость, недомогание...">
                    <span v-if="swShow1" class="small-warning">{{smallWarning}}</span>

                <div class="tst-inp">
                    <img class="mini-robot" src="../assets/mini-robot.svg" alt="">
                    <span class="mini-robot-text">Как давно это длится?</span>
                </div>
                <input v-model="question_2" class="test-input" type="text" name="" id="txtArea2" placeholder="Например: В течение недели, пары месяцев...">
                    <span v-if="swShow2" class="small-warning">{{smallWarning}}</span>
                <div class="tst-inp">
                    <img class="mini-robot" src="../assets/mini-robot.svg" alt="">
                    <span class="mini-robot-text">Опишите ваши ощущения:</span>
                </div>
                <textarea v-model="question_3" class="test-textarea" id="txtArea3" cols="30" rows="10" placeholder="Например: острая боль, тупая боль, разлитая боль, током стреляет, отдаёт в руку..."></textarea>
                    <span v-if="swShow3" class="small-warning">{{smallWarning}}</span>
                <div class="tst-inp">
                    <img class="mini-robot" src="../assets/mini-robot.svg" alt="">
                    <span class="mini-robot-text">При каких обстоятельствах это проявляется?</span>
                </div>
                <textarea v-model="question_4" class="test-textarea" id="txtArea4" cols="30" rows="10" placeholder="Например: утром, постоянно, вечером, после спорта, после еды..."></textarea>
                    <span v-if="swShow4" class="small-warning">{{smallWarning}}</span>
                <div class="tst-inp">
                    <img class="mini-robot" src="../assets/mini-robot.svg" alt="">
                    <span class="mini-robot-text">Как вы думаете, что могло быть причиной?</span>
                </div>
                <textarea v-model="question_5" class="test-textarea" id="txtArea5" cols="30" rows="10" placeholder="Например: Кажется после долгой поездки в автомобиле, после падения с лестницы"></textarea>
                    <span v-if="swShow5" class="small-warning">{{smallWarning}}</span>
                    <button @click="checkForm" class="test-form-button" type="button" >
                        {{testQuestion}}
                        <Spinner v-if="isLoadingResponse" />
                    </button>
            </form>
        </div>
        <div id="howIts" class="how-it-work">
            <span class="how-it-work-header-text">
                Как это работает?
            </span>
            <div class="description">
                <div class="wrapper-left-items">
                    <div class="number">
                        <img src="../assets/number.svg" alt="">
                    </div>
                    <div class="vert-line">
                        <img src="../assets/vert-line.svg" alt="">
                    </div>
                </div>
                <div class="description-text">
                    <span class="desc-head-text">Опишите ваши жалобы и симптомы как можно детальнее</span>
                    <span class="desc-sub-text">Чем детальнее вы опишите ваше состояние, тем лучше
                        искусственный интеллект поймёт, что вам порекомендовать.
                    </span>
                </div>
            </div>
            <div class="description">
                <div class="wrapper-left-items">
                    <div class="number">
                        <img src="../assets/number2.svg" alt="">
                    </div>
                    <div class="vert-line">
                        <img src="../assets/vert-line.svg" alt="">
                    </div>
                </div>
                <div class="description-text">
                    <span class="desc-head-text">Искусственный интеллект анализирует похожие случаи</span>
                    <span class="desc-sub-text">
                        AiBolit обучен на реальных кейсах. В его обучении участвовали десятки тысяч случаев.
                    </span>
                </div>
                
            </div>
            <div class="description">
                <div class="wrapper-left-items">
                    <div class="number">
                        <img src="../assets/number3.svg" alt="">
                    </div>
                    <div class="vert-line">
                        <img src="../assets/vert-line.svg" alt="">
                    </div>
                </div>
                <div class="description-text">
                    <span class="desc-head-text">Получите список исследований, которые вам вероятно стоит сделать</span>
                    <span class="desc-sub-text">
                        Вы можете пройти эти исследования, чтобы прийти с ними на первый приём к врачу и получить более развёрнутую консультацию.
                    </span>
                </div>
                
            </div>
            <div class="description">
                <div class="wrapper-left-items">
                    <div class="number">
                        <img src="../assets/number4.svg" alt="">
                    </div>
                    <div class="vert-line">
                        <!-- <img src="../assets/vert-line.svg" alt=""> -->
                    </div>
                </div>
                <div class="description-text">
                    <span class="desc-head-text">Получите скидку 5% на исследования в разных клиниках</span>
                    <img class="discount-img" src="../assets/discount.svg" alt="">
                    <span class="desc-sub-text">
                        А мы покажем список клиник, которые смогут вам помочь
                    </span>
                </div>
                
            </div>
            <a class="test-form-ref" href="#getStart"><button class="get-ready-button" type="button">Попробовать</button></a>
        </div>

    </div>
</template>

<script>
import Spinner from './Spinner.vue'

    export default {
        components: {
            Spinner
        },
        data() {
            return {

                questionData: [
                    {question_1: null},
                    {question_2: null},
                    {question_3: null},
                    {question_4: null},
                    {question_5: null}
                ],

                smallWarning: "Лучше не оставлять поля пустыми, тогда результат может быть не точным",
                swShow1: false,
                swShow2: false,
                swShow3: false,
                swShow4: false,
                swShow5: false,

                testQuestion: 'Показать результат',
                question: 'Показать результат',
                feedback: 'Готовим ответ',
                isLoadingResponse: false
            }
        },

        created() {
            document.addEventListener('keydown', this.resizeTxtArea)
        },

        beforeUnmount() {
            document.removeEventListener('keydown', this.resizeTxtArea)
        },
        methods: {

            resizeTxtArea(e) {
                e.target.style.height = 0
                e.target.style.height = e.target.scrollHeight - 40 + "px"
                if (e.target.id == 'txtSubArea') {
                    e.target.style.maxHeight = 90 + 'px'   //oграничение высoты TEXTAREA 
                }
            },

            getTest() {
                this.$emit('getTest')
            },

            checkForm(event) {
                this.question_1 == null ? this.swShow1 = true : this.swShow1 = false
                this.question_1 == null 
                    ? document.querySelector('#txtArea1').style.border = '1px solid #F45C69'
                    : document.querySelector('#txtArea1').style.border = '1px solid var( --inputs-borders )'
                this.question_2 == null ? this.swShow2 = true : this.swShow2 = false 
                this.question_2 == null 
                    ? document.querySelector('#txtArea2').style.border = '1px solid #F45C69'
                    : document.querySelector('#txtArea2').style.border = '1px solid var( --inputs-borders )'
                this.question_3 == null ? this.swShow3 = true : this.swShow3 = false 
                this.question_3 == null 
                    ? document.querySelector('#txtArea3').style.border = '1px solid #F45C69'
                    : document.querySelector('#txtArea3').style.border = '1px solid var( --inputs-borders )'
                this.question_4 == null ? this.swShow4 = true : this.swShow4 = false 
                this.question_4 == null 
                    ? document.querySelector('#txtArea4').style.border = '1px solid #F45C69'
                    : document.querySelector('#txtArea4').style.border = '1px solid var( --inputs-borders )'
                this.question_5 == null ? this.swShow5 = true : this.swShow5 = false 
                this.question_5 == null 
                    ? document.querySelector('#txtArea5').style.border = '1px solid #F45C69'
                    : document.querySelector('#txtArea5').style.border = '1px solid var( --inputs-borders )'

                if (this.question_1 != null &&
                    this.question_2 != null &&
                    this.question_3 != null &&
                    this.question_4 != null &&
                    this.question_5 != null
                    ) {
                        this.sendTestQuestion(event)
                    } 
            },

            sendTestQuestion(event) { 
                event.target.style.background = '#18B93C'
                event.target.style.color = 'var( --main-white )'
                event.target.style.fontSize = '14px'
                this.isLoadingResponse = true
                setTimeout(() => {
                    event.target.style.background = 'var(--main-white)'
                    this.testQuestion = this.question
                    event.target.style.fontSize = '16px'
                    this.getTest()
                },2000)
                this.testQuestion = this.feedback
            }
        },
    }
</script>

<style lang="css" scoped>
.condition-assessment {
    height: auto;
    width: 1160px;
    margin-top: 30px;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
}

@media screen and (max-width: 1280px) {
    .condition-assessment {
        height: auto;
        width: 90%;
        max-width: 1160px;
        margin-top: 30px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: flex-start;
    }
}

/* =============================================== */
.test-section {
    height: auto;
    width: 680px;
    background-color: var( --main-white );
    border-radius: 10px;
    padding-bottom: 50px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

@media screen and (max-width: 1280px) {
    .test-section {
        height: auto;
        width: 100%;
        /* max-width: 680px; */
        background-color: var( --main-white );
        border-radius: 10px;
        padding-bottom: 50px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
}
@-moz-document url-prefix() {
   .test-section {
        height: auto;
    }
} 
.test-header {
    height: 184px;
    width: 100%;
    /* background-color: rgb(233, 120, 120); */
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.test-header-text {
    height: 100%;
    width: 469px;
    margin-left: 50px;
    margin-top: 20px;
    /* background-color: rgb(150, 214, 125); */
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
}
@media screen and (max-width:1280px) {
    .test-header-text {
        height: 100%;
        width: 90%;
        margin-left: 50px;
        margin-top: 20px;
        /* background-color: rgb(150, 214, 125); */
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        align-items: flex-start;
    }
}
.head-text {
    width: 100%;
    margin-top: 20px;
    font-family: var( --font );
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 120%;
    text-align: start;
    color: var( --main-black );
    /* background-color: rgb(150, 214, 125); */
    display: flex;
    justify-content: flex-start;
    align-items: center;
}
@media screen and (max-width:1280px) {
    .head-text {
        width: 90%;
        margin-top: 20px;
        font-family: var( --font );
        font-style: normal;
        font-weight: 600;
        font-size: 24px;
        line-height: 120%;
        text-align: start;
        color: var( --main-black );
        /* background-color: rgb(150, 214, 125); */
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
}
@media screen and (max-width:800px) {
    .head-text {
        width: 100%;
        margin-top: 20px;
        font-family: var( --font );
        font-style: normal;
        font-weight: 600;
        font-size: 20px;
        line-height: 120%;
        text-align: start;
        color: var( --main-black );
        /* background-color: rgb(150, 214, 125); */
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
}
@media screen and (max-width:690px) {
    .head-text {
        height: 300px;
        width: 90%;
        margin-top: 20px;
        font-family: var( --font );
        font-style: normal;
        font-weight: 600;
        font-size: 24px;
        line-height: 120%;
        text-align: start;
        color: var( --main-black );
        /* background-color: rgb(150, 214, 125); */
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
}
@media screen and (max-width: 568px) {
    .head-text {
        height: 300px;
        width: 90%;
        margin-top: 20px;
        font-family: var( --font );
        font-style: normal;
        font-weight: 600;
        font-size: 20px;
        line-height: 120%;
        text-align: start;
        color: var( --main-black );
        /* background-color: rgb(150, 214, 125); */
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
}
@media screen and (max-width: 484px) {
    .head-text {
        height: 300px;
        width: 100%;
        margin-top: 20px;
        margin-left: -20px;
        font-family: var( --font );
        font-style: normal;
        font-weight: 600;
        font-size: 16px;
        line-height: 120%;
        text-align: start;
        color: var( --main-black );
        /* background-color: rgb(150, 214, 125); */
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
}
@media screen and (max-width: 375px) {
    .head-text {
        height: 300px;
        width: 90%;
        margin-top: -10px;
        margin-left: -20px;
        font-family: var( --font );
        font-style: normal;
        font-weight: 600;
        font-size: 14px;
        line-height: 120%;
        text-align: start;
        color: var( --main-black );
        /* background-color: rgb(150, 214, 125); */
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
}
@-moz-document url-prefix() {
    .head-text {
        height: 300px;
        min-width: 150px;
        margin-top: -10px;
        margin-left: -20px;
    }
}
.sub-text {
    margin-top: 10px;
    width: 100%;
    max-width: 469px;
    font-family: var( --font );
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 160%;
    color: var( --text-color );
}
@media screen and (max-width:800px) {
    .sub-text {
        margin-top: 10px;
        width: 100%;
        max-width: 469px;
        font-family: var( --font );
        font-style: normal;
        font-weight: normal;
        font-size: 14px;
        line-height: 160%;
        color: var( --text-color );
    }
}
@media screen and (max-width:690px) {
    .sub-text {
        display: none;
    }
}

@-moz-document url-prefix() {
    .sub-text {
        margin-top: 20px;
        width: 469px;
        font-family: var( --font );
        font-style: normal;
        font-weight: normal;
        font-size: 16px;
        line-height: 160%;
        color: var( --text-color );
    }
}  
.test-header-img {
    height: 100%;
    width: 118px;
    margin-right: 39px;
    /* background-color: rgb(150, 214, 125); */
    display: flex;
    justify-content: center;
    align-items: center;
}
.header-img {
    width: 150%;
}
@-moz-document url-prefix() {
    .header-img {
        min-width: 80px;
        height: 120px;
        margin-top: 30px;
    }
}
@media screen and (max-width:690px) {
    .header-img {
        width: 120%;
        margin-top: 30px;
        margin-right: 20px;
        padding-left: 20px;
    }
}

@media screen and (max-width: 1280px) {
    .test-header-img {
        height: 100%;
        width: 118px;
        margin-right: 59px;
        /* background-color: rgb(150, 214, 125); */
        display: flex;
        justify-content: center;
        align-items: center;
    }
}
@media screen and (max-width: 800px) {
    .test-header-img {
        height: 100%;
        width: 110px;
        margin-right: 49px;
        margin-bottom: 20px;
        /* background-color: rgb(150, 214, 125); */
        display: flex;
        justify-content: center;
        align-items: center;
    }
}
/* ====================Test Form=========================== */
.test-form {
    height: 100%;
    width: 580px;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
}
@media screen and (max-width: 1280px) {
    .test-form {
        height: 100%;
        width: 90%;
        /* max-width: 580px; */
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
    }
}
@media screen and (max-width: 768px) {
    .test-form {
        height: 100%;
        width: 100%;
        max-width: 580px;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
    }
}
@media screen and (max-width: 720px) {
    .test-form {
        height: 100%;
        width: 80%;
        max-width: 580px;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
    }
}
.mini-robot-text {
    height: 42px;
    width: auto;
    padding-left: 10px;
    padding-right: 10px;
    margin-left: 5px;
    font-family: var( --font );
    font-style: normal;
    font-weight: 500;
    font-size: 18px;
    line-height: 120%;
    color: var( --text-color );
    background-color: var( --say-background );
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
}
@media screen and (max-width: 660px) {
    .mini-robot-text {
        font-size: 14px;
    }
}
@media screen and (max-width: 522px) {
    .mini-robot-text {
        font-size: 12px;
    }
}

@-moz-document url-prefix() {
    .mini-robot-text {
        background-color: var( --say-moz-background );
    }
}  
.tst-inp {
    height: 42px;
    width: 100%;
    margin-top: 40px;
    margin-bottom: 15px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
}
.test-input {
    font-family: var( --font );
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 120%;
    min-height: 64px;
    width: 100%;
    padding-left: 20px;
    padding-right: 20px;
    border: 1px solid var( --inputs-borders );
    outline: none;
    box-sizing: border-box;
    border-radius: 7px;
    color: var( --text-color );
}
@media screen and (max-width: 768px) {
    
}
.test-input::placeholder {
    color: var( --placeholder-color );
    font-family: var( --font );
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 120%;
}
@media screen and (max-width: 592px) {
    .test-input::placeholder {
        width: 100%;
        font-size: 12px;
        white-space: pre-wrap;
        margin-bottom: 20px;
    }
}
.test-textarea {
    height: 44px;
    display:  block;
    font-family: var( --font );
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 120%;
    padding-bottom: 20px;
    padding-top: 20px;
    min-height: 44px;
    padding-left: 20px;
    padding-right: 20px;
    width: 92%;
    resize: none;
    border: 1px solid var( --inputs-borders );
    outline: none;
    border-radius: 7px;
    color: var( --text-color );
}
.test-textarea::placeholder {
    width: 400px;
    padding-top: 0px;
    color: var( --placeholder-color );
    font-family: var( --font );
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 120%;
}
@media screen and (max-width: 592px) {
    .test-textarea::placeholder {
        width: 100%;
        font-size: 12px;
    }
}
.test-form-button {
    width: 580px;
    height: 65px;
    min-height: 65px;
    margin-top: 30px;
    border: none;
    outline: none;
    background: var( --main-yellow );
    border-radius: 10px;
    font-family: var( --font );
    font-style: normal;
    font-weight: 600;
    font-size: 18px;
    line-height: 140%;
    text-align: center;
    color: var( --main-black );
    display: flex; 
    justify-content: center;
    align-items: center;
}
.test-form-button:hover {
    background: var(  --hover-dark );
    color: var( --main-white );
}

@media screen and (max-width: 768px) {
    .test-form-button {
        height: 50px;
        width: 260px;
        padding-left: 20px;
        padding-right: 20px;
    }
    .test-form-button:hover {
    background: var(  --hover-dark );
    color: var( --main-white );
}
}
.test-form-ref {
    text-decoration: none;
    color: var( --main-black );
}
/* ====================Test Form=========================== */

/* =============================================== */
.how-it-work {
    height: 920px;
    width: 450px;
    background-color: var( --main-white );
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
}
@media screen and (max-width: 1280px) {
    .how-it-work {
        height: 1020px;
        width: 100%;
        max-width: auto;
        margin-top: 30px;
        background-color: var( --main-white );
        border-radius: 10px;
        display: flex; 
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
    }
}
.how-it-work-header-text {
    height: 29px;
    width: 386px;
    margin-top: 37px;
    margin-bottom: 54px;
    margin-left: 40px;
    display: flex;
    font-family: var( --font );
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 120%;
    color: var( --main-black );
}
@media screen and (max-width: 1280px) {
    .how-it-work-header-text {
        height: 29px;
        width: 100%;
        margin-top: 37px;
        margin-bottom: 54px;
        margin-left: 0px;
        display: flex;
        font-family: var( --font );
        font-style: normal;
        font-weight: 600;
        font-size: 24px;
        line-height: 120%;
        color: var( --main-black );
        display: flex; 
        justify-content: center;
        align-items: center;
    }
}
.description {
    height: 196px;
    width: 350px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
}
@media screen and (max-width: 1280px) {
    .description {
        height: 196px;
        width: 70%;
        margin-left: -30px;
        display: flex;
        justify-content: flex-start;
    }
}
.wrapper-left-items {
    height: 196px;
    width: 29px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.number {
    height: 29px;
    width: 29px;
    display: flex;
    justify-content: center;
    align-items: center;
}
.vert-line {
    height: 167px;
    width: 4px;
    display: flex;
    justify-content: center;
    align-items: center;
}
/* =================================== */
.description-text {
    height: 100%;
    width: 300px;
    margin-left: 11px;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
}
@media screen and (max-width: 1280px) {
    .description-text {
        height: 100%;
        min-width: 190px;
        width: 100%;
        margin-left: 11px;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;
    }
}

.desc-head-text {
    height: 42px;
    width: 310px;
    font-family: var( --font );
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 130%;
    color: var( --main-black );
}
@media screen and (max-width: 1280px) {
    .desc-head-text {
        height: 42px;
        width: 100%;
        font-family: var( --font );
        font-style: normal;
        font-weight: 600;
        font-size: 16px;
        line-height: 130%;
        color: var( --main-black );
    }
}
@media screen and (max-width: 576px) {
    .desc-head-text {
        height: 42px;
        width: 100%;
        font-family: var( --font );
        font-style: normal;
        font-weight: 600;
        font-size: 12px;
        line-height: 130%;
        color: var( --main-black );
    }
}
.desc-sub-text {
    height: 68px;
    width: 310px;
    margin-top: 10px;
    font-family: var( --font );
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 140%;
    color: var( --text-color );
}

@media screen and (max-width: 1280px) {
    .desc-sub-text {
        height: 68px;
        width: 100%;
        margin-top: 10px;
        font-family: var( --font );
        font-style: normal;
        font-weight: normal;
        font-size: 16px;
        line-height: 140%;
        color: var( --text-color );
    }
}
@media screen and (max-width: 576px) {
    .desc-sub-text {
        height: 68px;
        width: 100%;
        margin-top: 20px;
        font-family: var( --font );
        font-style: normal;
        font-weight: normal;
        font-size: 12px;
        line-height: 140%;
        color: var( --text-color );
    }
}
.discount-img {
    height: 49px;
    width: 143px;
    padding-top: 10px;
}


.get-ready-button {
    height: 50px;
    width: 280px;
    margin-top: 20px;
    background-color: var( --main-yellow );
    border-radius: 10px;
    font-family:  var( --font );
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 140%;
    text-align: center;
    outline: none;
    border: none;
}

    .get-ready-button {
        display: none;
        height: 50px;
        width: 260px;
        margin-top: 20px;
        background-color: var( --main-yellow );
        border-radius: 10px;
        font-family:  var( --font );
        font-style: normal;
        font-weight: bold;
        font-size: 16px;
        line-height: 140%;
        text-align: center;
        outline: none;
        border: none;
    }
@media screen and (max-width: 1280px) {
    .get-ready-button {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 50px;
        width: 260px;
        margin-top: 20px;
        background-color: var( --main-yellow );
        border-radius: 10px;
        font-family:  var( --font );
        font-style: normal;
        font-weight: bold;
        font-size: 16px;
        line-height: 140%;
        text-align: center;
        outline: none;
        border: none;
    }
}



.small-warning {
    height: 20px;
    width: 100%;
    padding-left: 20px;
    margin-top: 6px;
    font-family:  var( --font );
    font-style: normal;
    font-weight: normal;
    font-size: 12px;
    line-height: 100%;
    color: #F45C69;
    display: flex;
    justify-content: flex-start;
    align-items: flex-start;
}
@media screen and (max-width: 612px) {
    .small-warning {
        padding-left: 10px;
        font-size: 9px;
    }
}
@media screen and (max-width: 452px) {
    .small-warning {
        text-align: center;
    }
}
</style>
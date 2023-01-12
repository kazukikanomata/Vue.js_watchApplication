<template>
    <div class="container">
        <div class="clock">
            <div class="date">
                <p>{{ year }}/ {{ month }}/{{ day }}</p>
            </div>
            <div class="time">
                <p>{{ hours }}:{{ minutes }}<span class="second">:{{ seconds }}</span></p>
            </div>
            <div class="button" v-on:click="showMessage()">
                <p>10秒後にアラートを設定</p>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        name: "ClockScreen",
        // dataはデータを定義する場所
        data() {
            return{
                // 現在の日時を保持する。
                date: new Date(),
            };
        },
        // 保持したデータを加工する役割
        // 画面の情報を更新するたびに自動で取得される
        computed: {
            // 年
            year() {
                return this.date.getFullYear();
            },
            // 月
            // 0月から11月から取ってくる
            month(){
                return this.date.getMonth()+1;
            },
            // 日
            day(){
                return this.dateTimePadding(this.date.getDate());
            },
            // 時間
            hours(){
                return this.dateTimePadding(this.date.getHours());
            },
            // 分
            minutes(){
                return this.dateTimePadding(this.date.getMinutes());
            },
            // 秒
            seconds(){
                return this.dateTimePadding(this.date.getSeconds());   
            }
        },
        mounted(){
            //画面に表示される時に一番最初に読み込まれる。
            //ライフサイクル
            this.setDate();
            // １秒ごとにsetDate()を実行する
            setInterval(()=> this.setDate(), 1000);
        },
        methods: {
            // 日時を二桁に
            dateTimePadding(num){
                return ("0" + num ).slice(-2);
            },
            // 現在日時をセット
            setDate(){
                this.date = new Date();
            },
            showMessage(){
                window.setTimeout(()=>{
                    alert("10秒経過しました");
                }, 10000);
            },
        },
    }



</script>

<style scoped>
.container {
    height: 100%;
    display: flex;
    flex-flow: column;
    justify-content: center;
    align-items: center;
    background-color: black;
}
.p{
    margin: 0px;
    color: white;
}

.date,
.time{
    font-weight: 700;
    color: green;
}
.button{
    border: 1px solid #fcfcfc;
    text-align: center;
    padding: 10px 0;
    color: #fcfcfc;
    cursor: pointer;
}
</style>
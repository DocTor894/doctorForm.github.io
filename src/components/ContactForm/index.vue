<template>
    <div class="form">
        <h2 class="form-title">Создание клиента</h2>


        <div class="form-group">
            <input type="text" placeholder="Фамилия*" v-model="lastname">
            <p class="status" v-if="!$v.lastname.required">Заполните поле</p>
            <p class="status" v-if="!$v.lastname.alpha">Фамилия должна содержать только русские буквы</p>
        </div>
        
        <div class="form-group">
            <input type="text" placeholder="Имя*" v-model="firstname">
            <p class="status" v-if="!$v.firstname.required">Заполните поле</p>
            <p class="status" v-if="!$v.lastname.alpha">Имя должно содержать только русские буквы</p>
        </div>
        
        <div class="form-group">
            <input type="text" placeholder="Отчество" v-model="patronymic">
            <p class="status" v-if="!$v.patronymic.alpha">Отчество должно содержать только русские буквы</p>
        </div>
        
        <div class="form-group date">
            <p class="date-title">Дата рождения:*</p>
            <input type="date" v-model="birthday">
            <p v-if="!$v.birthday.required" class="status">Введите дату</p>
        </div>
        
        <div class="form-group">
            <input type="text" placeholder="Телефон*" v-model="phone">
            <p class="status" v-if="!$v.phone.required">Введите номер телефона</p>
            <p class="status" v-if="!$v.phone.validFormat">Номер должен начинаться с 7 и содержать 11 символов</p>
        </div>
        
        <div class="form-group gender">
            <p class="gender">Пол:</p>
            <p>
                <input type="radio" id="male" name="gender" v-model="gender">
                <label for="male">Мужской</label>
            </p> 
            <p>
                <input type="radio" id="female" name="gender" v-model="gender">
                <label for="female">Женский</label>
            </p> 
        </div>

        <div class="form-group">
            <input type="text" placeholder="Индекс" v-model="index">
        </div>

        <div class="form-group">
            <input type="text" placeholder="Страна" v-model="country">
        </div>

        <div class="form-group">
            <input type="text" placeholder="Область" v-model="region">
        </div>

        <div class="form-group">
            <input type="text" placeholder="Город*" v-model="city">
            <p class="status" v-if="!$v.city.required">Заполните поле</p>
        </div>

        <div class="form-group">
            <input type="text" placeholder="Улица" v-model="street">
        </div>

        <div class="form-group">
            <input type="text" placeholder="Дом" v-model="house">
        </div>

        <div class="form-group">
            <p>
                <select class="select" v-model="document">
                    <option disabled value="">Тип документа*</option>
                    <option value="pas">Паспорт</option>
                    <option>Свидетельство о рождении</option>
                    <option>Водительское удостоверение</option>
                </select>
            </p>
            <p class="status" v-if="!$v.document.required">Выберите документ</p>
        </div>

        <div class="form-group">
            <input type="text" placeholder="Серия" v-model="series">
        </div>

        <div class="form-group">
            <input type="text" placeholder="Номер" v-model="number">
        </div>

        <div class="form-group">
            <input type="text" placeholder="Кем выдан" v-model="subdivision">
        </div>

        <div class="form-group date">
            <p class="date-title">Дата выдачи:*</p>
            <input type="date" v-model="issueDate">
            <p v-if="!$v.issueDate.required" class="status">Введите дату</p>
        </div>


        <div class="form-group group">
            <p class="gender">Группа клиентов:</p>
            <p>
                <input type="radio" id="vip" name="group" value="VIP" v-model="group">
                <label for="vip">VIP</label>
            </p> 
            <p>
                <input type="radio" id="problem" name="group" value="Проблемные" v-model="group">
                <label for="problem">Проблемные</label>
            </p> 
            <p>
                <input type="radio" id="oms" name="group" value="ОМС" v-model="group">
                <label for="oms">ОМС</label>
            </p>
            <p v-if="!$v.group.required" class="status">Выберите группу</p>
        </div>

        <div class="form-group">
            <p>
                <select class="select" v-model="doctor">
                    <option disabled value="">Лечащий врач</option>
                    <option value="pas">Иванов</option>
                    <option>Захаров</option>
                    <option>Чернышева</option>
                </select>
            </p>
            <p class="status" v-if="!$v.doctor.required">Выберите врача</p>
        </div>

        <div class="from-group check">
            <p>
                <input type="checkbox" id="check" class="check" v-model="sms">
                <label for="check">Не отправлять СМС</label>
            </p>
        </div>

        <div class="from-group btn" @click="submit()">
            <button >Создать</button> 
        </div>
    </div>
</template>

<script>
import { required, minLength } from 'vuelidate/lib/validators'

export default {
    name: 'contactForm',
    data: () => ({
        lastname: '',
        firstname: '',
        patronymic: '',
        birthday: '',
        phone: '',
        gender: '',
        index: '',
        country: '',
        region: '',
        city: '',
        street: '',
        house: '',
        document: '',
        series: '',
        number: '',
        subdivision: '',
        issueDate: '',
        group: '',
        doctor: '',
        sms: false,

    }),
    methods: {
        submit() {
            if(!this.$v.$invalid) {
                alert('Клиент создан');
            }
        }
    },
    validations: {
        lastname: {
            required,
            alpha: val => /^[а-яё]*$/i.test(val),
        },
        firstname: {
            required,
            alpha: val => /^[а-яё]*$/i.test(val),
        },
        patronymic: {
            alpha: val => /^[а-яё]*$/i.test(val),
        },
        birthday: {
            required,
        },
        phone: {
            required,
            validFormat: val => /^[7]\d{10}$/.test(val),
        },
        city: {
            required,
        },
        document: {
            required,
        },
        issueDate: {
            required,
        },
        group: {
            required,
        },
        doctor: {
            required,
        },
    }
}
</script>

<style lang="sass">
$error: #F36363

.form
    background: #FFFFFF
    width: 100%
    margin: auto
    padding: 20px
    border-radius: 5px
    display: grid
    grid-template-columns: 1fr 1fr 1fr
    grid-gap: 20px

    .form-title
        grid-column: 1/4
        text-align: center

    .form-group
        display: flex
        flex-direction: column
        color: #303030

        & input, select
            padding: 10px
            border: 1px solid #A5A5A5
            border-radius: 5px
            outline: none

            &.invalid, select.invalid
                border-color: $error
            
            &.invalid::placeholder
                color: $error

            &:focus
                border: 1px solid #F9C73B

        & .status
            color: $error

        &.date
            display: flex
            flex-direction: row
            align-items: center

            & .status
                margin-left: 10px

    .gender, .group
        flex-direction: row

        & p
            margin-right: 20px

        & input
            margin-right: 5px

    .group
        grid-column: 1/3
        display: flex
        justify-content: center
        align-items: center

    .check, .btn
        grid-column: 1/4
        text-align: center
    
    .btn button
        padding: 10px 20px
        background: #F9C73B
        border: 1px solid #F9C73B
        border-radius: 5px
        color: white
    
    .btn button:hover
        cursor: pointer
        background: #FFFFFF
        border: 1px solid #F9C73B
        color: #F9C73B

</style>
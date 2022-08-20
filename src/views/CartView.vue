<template>
    <h1>Kundvagn</h1>
    <div class="main-wrapper">
        <img class="image" :src="'/pictures/' + image" width="350" height="350">
        <div class="container-info">
            <h1>{{ productName }}</h1>
            <p class="wrap-description">{{ description }}</p>
        </div>
    </div>

    <div class="loader-1 center" id="loader"><span></span></div>

    <div class="popup">
        <span class="popuptext" id="myPopup">
            <h1>TACK FÖR DITT KÖP AV {{ productName }}</h1>
            <ul>
                <img style="align-center" :src="'/pictures/' + image" width="150" height="150">
                <li>Förnamn: {{ fname }}</li>
                <li>------------------------------------------</li>
                <li>Efternamn: {{ lname }}</li>
                <li>------------------------------------------</li>
                <li>Telefonnummer: {{ phonenumber }}</li>
                <li>------------------------------------------</li>
                <li>Email: {{ email }}</li>
                <li>------------------------------------------</li>
                <li>Adress: {{ adress }}</li>
                <li>------------------------------------------</li>
                <li>Stad: {{ city }}</li>
                <li>------------------------------------------</li>
                <li>Postnummer: {{ zipcode }}</li>
                <li>------------------------------------------</li>
            </ul>
            <button class="btn" @click="redirect()">Ta mig tillbaka till startsidan</button>
        </span>
    </div>

    <form class="row">
        <div class="container">
            <h1>Fakturerings adress</h1>
            <label for="fname">Förnamn</label>
            <input type="text" id="fname" placeholder="Förnamn" v-model="fname">
            <label for="lname">Efternamn</label>
            <input type="text" id="lname" placeholder="Efternamn" v-model="lname" />
            <label for="phonenumber">Telefonnummer</label>
            <input type="text" key="phonenumber" placeholder="Telefonnummer" v-model="phonenumber" />
            <label for="email">Email</label>
            <input pattern="^[^\s@]+@([^\s@.,]+\.)+[^\s@.,]{2,}$" title="Är inte en gilig email adress" type="email"
                id="email" placeholder="Email" v-model="email" />
            <label for="street">Adress</label>
            <input type="text" id="street" placeholder="Adress" v-model="adress" />
            <label for="city">Stad</label>
            <input type="text" id="city" placeholder="Stad" v-model="city" />
            <label for="zip">Postnummer</label>
            <input type="text" id="zip" placeholder="151 60" v-model="zipcode" />
        </div>
        <div class="container">
            <h1>Kort Information</h1>
            <label>Namn på kortet</label>
            <input type="text" placeholder="Namn på kortet">
            <label>Kortnummer</label>
            <input type="text" placeholder="4587 2671 4782 6987">
            <label>Exp datum</label>
            <input type="text" placeholder="11/22">
            <label>CVV</label>
            <input type="text" placeholder="321">
            <button @click="submit()" class="btn">Betala</button>
        </div>
    </form>
</template>


<script>

export default {

    data() {
        return {
            //items to display
            id: 0,
            productName: "",
            price: 0,
            description: "",
            image: null,

            //buyValues
            fname: "",
            lname: "",
            phonenumber: "",
            email: "",
            adress: "",
            city: "",
            zipcode: "",

            //creditcard
            cardName: "",
            cardNumber: 0,
            expdate: "",
            cvv: 0,
        }
    },
    created() {
        const id = this.$route.params.id
        fetch('http://localhost:5050/api/Products/' + id)
            .then(data => data.json())
            .then(products => {
                console.log(id)
                this.productName = products.name,
                this.price = products.price,
                this.description = products.description
                this.image = products.image
            })
    },
    methods: {
        submit() {
            myFunction()

        },
        redirect() {
            this.$router.push('/')
        }
    }
}

function myFunction() {
    var popup = document.getElementById("myPopup");
    popup.classList.toggle("show");
}
</script>

<style scoped>
ul
{
    text-align: left;
    font-size: 20px;
}

li
{
    list-style-type: none;
}

.main-wrapper
{
    display: -ms-flexbox;
    /* IE10 */
    display: flex;
    -ms-flex-wrap: wrap;
    /* IE10 */
    flex-wrap: wrap;
    justify-content: center;
}

.image
{
    margin-left: -21%;
    margin-right: 75px;
}

.container-info
{
    display: flex;
    flex-flow: column;
    background-color: #f2f2f2;
    padding: 5px 20px 15px 20px;
    border: 1px solid lightgrey;
    border-radius: 3px;
    align-items: center;
    width: 40%;
    float: left;
}

.wrap-description
{
    width: 50%;
    text-align: center;
}

.row
{
    display: -ms-flexbox;
    /* IE10 */
    display: flex;
    -ms-flex-wrap: wrap;
    /* IE10 */
    flex-wrap: wrap;
    justify-content: center;
    margin-top: -600px;
    margin-bottom: 50px;

}

.container
{
    display: flex;
    flex-flow: column;
    background-color: #f2f2f2;
    padding: 5px 20px 15px 20px;
    border: 1px solid lightgrey;
    border-radius: 3px;
    align-items: center;
    width: 40%;
    float: left;
}

input[type=text],
[type=email]
{
    width: 80%;
    margin-bottom: 20px;
    padding: 12px;
    border: 1px solid #ccc;
    border-radius: 3px;
}


label
{
    margin-bottom: 10px;
}

.btn
{
    background-color: aquamarine;
    color: black;
    padding: 12px;
    margin: 10px 0;
    border: none;
    width: 100%;
    border-radius: 3px;
    cursor: pointer;
    font-size: 17px;
}

.btn:hover
{
    opacity: 0.75;
}


/*POPUP*/
/* Popup container */
.popup
{

    display: flex;
    width: 100%;
    height: 100%;
}

/* The actual popup (appears on top) */
.popup .popuptext
{
    visibility: hidden;
    background-color: lightgray;
    color: black;
    text-align: center;
    border-radius: 6px;
    width: 100%;
    height: 100%;
    padding: 8px 0;
    z-index: 1;
}

/* Toggle this class when clicking on the popup container (hide and show the popup) */
.popup .show
{
    visibility: visible;
    -webkit-animation: fadeIn 1s;
    animation: fadeIn 1s
}

/* Add animation (fade in the popup) */
@-webkit-keyframes fadeIn
{
    from
    {
        opacity: 0;
    }

    to
    {
        opacity: 1;
    }
}

@keyframes fadeIn
{
    from
    {
        opacity: 0;
    }

    to
    {
        opacity: 1;
    }
}
</style>
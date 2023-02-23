<template>
    <h3>Welcome to the link Shorter</h3>
    <h3>paste the link you want to shorten here below:</h3>
    <input type="text" ref="linkToShorten" placeholder="https://www.youtube.com/watch?v=gwDoRPcPxtc" value=""/>
    <input type="button" value="shorten Link" name="shorten" @click="userAction"> 
    <div id="error" v-if="this.gotAnError">
        <p>{{this.errors}}</p>   
    </div>
    <div id="result" v-if="this.validResult">
        <p>Here's your result:</p>
        <a :href="this.result" target="_blank">{{this.result}}</a>
    </div>    
</template>

<script>
export default {
    name: 'Shortner',
    data: function() {
        return {
            result: "",
            validResult: false,
            accessToken: "af1ba18f5c0f65d0848c55e678a9e04c7ce9fde0",
            validLink: false,
            gotAnError: false,
            errors: "",
        }
    },

    methods: {
        
        isInvalidUrlRegex (urlString) {
            var urlPattern = new RegExp(
                '^(https?:\\/\\/)?'+ // validate protocol
                '((([a-z\\d]([a-z\\d-]*[a-z\\d])*)\\.)+[a-z]{2,}|'+ // validate domain name
                '((\\d{1,3}\\.){3}\\d{1,3}))'+ // validate OR ip (v4) address
                '(\\:\\d+)?(\\/[-a-z\\d%_.~+]*)*'+ // validate port and path
                '(\\?[;&a-z\\d%_.~+=-]*)?'+ // validate query string
                '(\\#[-a-z\\d_]*)?$','i'); // validate fragment locator
	        return !urlPattern.test(urlString); //returns true is the string is not valid, false if it's valid
	    },
        
        showError(errorValue){
            this.gotAnError=true;
            this.errors=errorValue;

            //removes the error after 3 seconds
            setTimeout(() => this.gotAnError=false, 3500);
        }, 
        
        getlink(){
            return this.$refs.linkToShorten.value;
        },

        checkLink() {
            let link=this.getlink();

            if (link.length == 0)
            {   
                this.showError("No empty textbox allowed, You have to write a link in the textbox....");
                //console.log("No empty textbox allowed, You have to write a link in the textbox....");
                return false;
            } else if (link.length > 0 && this.isInvalidUrlRegex(link)) {
                this.showError("Verify your link please....");
                //console.log("link is not a correct format!");
                return false;
            } else {
                this.gotAnError=false;
                return true;
            }
        },

        async userAction() {
            this.checkLink() ? console.log("link is valid, proceeding to shortage...") : '';
            await fetch("https://api-ssl.bitly.com/v4/shorten", {
                method: "POST",
                headers: {
                    'Authorization': "Bearer "+this.accessToken,
                    'Content-Type': 'application/json'
                }, 
                body: JSON.stringify({
                    "long_url": this.getlink()
                })
                //we construct the request (adding the headers, the url, the method) in the fetch function above 
                //then we check if the response we get has an error or not
                }).then(response => { 
                if(response.ok){
                    return response.json() 
                } else{
                    //console.log("Server returned " + response.status + " : "+ response.statusText );
                    //console.log(response.headers.get('Authorization'))
                    console.error("There was an error during the API request....");
                }                
            })
            .then(response => {
                try{
                this.result = response.link; 
                this.validResult = true;
                } catch (TypeError){
                    console.error("Your link may be empty or incorrect, verify it....");
                }
            })
            .catch(err => {
                console.error(err);
            });
            
        },
    },
}
</script>

<style scoped>
    h3{
        font-size: 2.5em;
    }

    input[type="text"]{
        border-radius: 5px;
        padding: 3.5em 2.5em;
        font-size: 24pt;
        
    }

    input[type="button"]{
        font-size: 24pt;
    }

    div#result{
        border: 1cm solid green;
        padding: 55px;
        background-color: green;
        color: azure;
    }

    div#error{
        border: 1cm solid red;
        padding: 15px;
        background-color: red;
        color: azure;
    }
</style>
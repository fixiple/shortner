<template>
    <div id="footer">
        <p> Made with ❤ by <a href="https://github.com/fixiple">Fixiple</a> using Vue3</p>
    </div>
</template>
<script>
export default {
    name: 'customfooter'
}
</script>
<style scoped>
    #footer{
        font-size: 15px;
        background-color: rgb(0, 236, 253);
        color: black;
        text-align: center;
        margin-top: 15px;
        
        /*To keep the footer at bottom of page and with full width.*/
        position:fixed;
        bottom:0; 
        left: 0;
        width:100%; 

    }
</style>
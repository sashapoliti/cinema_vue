<template>
    <footer>
        <div class="first">
            <img src="/images/animated-c.gif" alt="placeholder">
            <h2 class="text-center m-auto text-white" id="title">Immergiti nell'universo cinematografico di Boolean.</h2>

        </div>
        <div class="second ">
            <div class="left">
                <div class="p-3 me-5">
                    <h5>SOCIAL</h5>
                    <ul class="list-unstyled text-center">
                        <li><a class="text-decoration-none" href="https://www.instagram.com/"><i class="fa-brands fa-instagram"></i> instagram</a></li>
                        <li><a class="text-decoration-none" href="https://www.facebook.com/?locale=it_IT"><i class="fa-brands fa-facebook"></i> facebook</a></li>
                        <li><a class="text-decoration-none" href="https://x.com/i/flow/login"><i class="fa-brands fa-twitter"></i> twitter</a></li>
                        <li><a class="text-decoration-none" href="https://www.tiktok.com/login"><i class="fa-brands fa-tiktok"></i> tiktok</a></li>
                    </ul>
                </div>
                <div class="p-3 mx-5">
                    <h5>NOTE LEGALI</h5>
                    <ul class="list-unstyled text-center">
                        <li><a class="text-decoration-none" href="">Privacy policy</a></li>
                        <li><a class="text-decoration-none" href="">Cookie policy</a></li>
                        <li><a class="text-decoration-none" href="">Condizioni di utilizzo</a></li>
                        <li><a class="text-decoration-none" href="">Regolamenti</a></li>
                        
                    </ul>
                </div>
                <div class="p-3 mx-5">
                    <h5>CINEX</h5>
                    <ul class="list-unstyled text-center">
                        <li><a class="text-decoration-none" href="">chi siamo</a></li>
                        <li><a class="text-decoration-none" href="">i nostri cinema</a></li>
                    </ul>
                </div>
            </div>
            <div class="right d-flex align-items-center justify-content-center">
                <img src="/images/logo.png" alt="">
            </div>
        </div>
    </footer>
</template>

<script>
export default {
    name: "FooterComponent"
}
</script>

<style lang="scss" scoped>
@use '../assets/styles/partials/_variables.scss' as *;

footer {
    height: 600px;


    .first {
        height: 300px;
        display: flex;
        background-color: $color-blue;
        padding: 15px;
    }


    .second {

        height: 300px;
        display: flex;
        background-color: #E8B757;
        color: white;

        .left {
            width: 50%;
            display: flex;

            h5 {
                text-align: center;
            }

            ul {


                li {
                    padding: 5px 20px;
                    i{
                        font-size: 25px;
                    }

                    &:hover {
                        background-color: rgba(188, 188, 188, 0.059);
                        cursor: pointer;
                    }

                    &:hover a {
                        color: white;

                    }


                    a {
                        color: #E87E66;



                    }
                }
            }

        }

        .right {
            width: 50%;
            padding: 15px;
        }


    }
}
</style>
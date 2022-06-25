<script context="module">
    export async function load({fetch, params}) {
        const res = await fetch(`https://api.themoviedb.org/3/movie/${params.id}?api_key=88637c22a27d11937d1168157cf81ce9&language=en-US`);
    
    const movieDetail = await res.json();
    
    if(res.ok) {
        return{
            props: { movieDetail }
        };
    }
}
</script> 

<script>
    export let movieDetail;
    console.log(movieDetail);
    import {fly} from 'svelte/transition';
</script>

<div class="movie-detail" in:fly={{y: 50, duration: 400, delay:500}} out:fly={{duration: 500}}>
    <div class="img-container">
        <img src={'https://image.tmdb.org/t/p/original' + movieDetail.backdrop_path} alt={movieDetail.title}>
    </div>
    <div class="txt-container">
        <h1>{movieDetail.title}</h1>
        <p class="overview">{movieDetail.overview}</p>
        <p>
            <span>Release date:</span>
            {movieDetail.release_date} <br />
            <span>Budget:</span> ${movieDetail.budget}<br />
            <span>Rating:</span>
            {movieDetail.vote_average}<br />
            <span>Runtime:</span>
            {movieDetail.runtime}mins
        </p>
   </div> 
</div>

<style>
    h1 {
        padding: 1rem 0rem 2rem;

    }
    p {
        padding: 1rem 0rem;
    }
    .img-container {
        widows: 100%;
    }
    img {
        width: 100%;
        border-radius: 1rem;
    }
    .movie-detail {
        margin: 2rem 20%;
    }
    span {
        font-weight: bold;
    }

</style>



<script>
    export let name;
    export let rating;
    export let comment;
  </script>
  
  <div class="review">
    <h3>{name}</h3>
    <p>Rating: {rating} / 5</p>
    <p>{comment}</p>
  </div>
  
  <style>
    .review {
      display: grid;
      background-color: #090b13;
      padding: 1rem;
      margin: 1rem;
      border-radius: 1rem;
    }
  
    .review h3 {
      margin: 0;
      font-size: 1.2rem;
    }
  
    .review p {
      margin: 0.5rem 0;
    }
  </style>
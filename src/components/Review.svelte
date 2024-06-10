<script>
    export let name;
    export let rating;
    export let comment;
    export let image;
  </script>
  
  <div class="review">
    <div class="review-top">
    <div class="image-container">
      <img src={image} alt={name}>
    </div>
    
    <div>
      <h3>{name}</h3>
      <p>Rating: {rating} / 5</p>
   </div>
   </div>
    <p class="black-box">{comment}</p>
  </div>
  
  <style>
    .review {
      display: grid;
      padding: 1rem;
      margin: 1rem;
      border-radius: 1rem;
    }
    .review-top {
      display: flex;
      align-items: center;
      gap: 2rem;
      margin-bottom: 1rem;
    }
    .black-box {
      background-color: #0084ff;
      border-radius: 1.5rem;
      border-top-left-radius: 0.2rem;
      padding: 1rem;
    }
    .review h3 {
      margin: 0;
      font-size: 1.2rem;
    }
  
    .review p {
      margin: 0.5rem 0;
      line-height: 1.5rem;
    }
    .image-container {
      height: 8rem;
      width: 8rem;
      border-radius: 50%;
      overflow: hidden;
    }
    .image-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
  }
  </style>
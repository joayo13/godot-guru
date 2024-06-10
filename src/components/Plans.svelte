<script>
    // Add any script logic here if needed
  </script>
  
  <style>
    .plans-container {
      display: flex;
      padding-left: 10rem;
      padding-right: 10rem;
      justify-content: space-around;
      flex-wrap: wrap;
    }
  
    .plan {
      border-radius: 1rem;
      background-color: rgba(0,0,0,0.5);
      padding: 20px;
      margin: 10px;
      flex: 1;
      min-width: 250px;
      max-width: 300px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      transition: transform 0.3s, box-shadow 0.3s;
    }
  
    .plan:hover {
      transform: translateY(-5px);
      box-shadow: 0 8px 16px rgba(0,0,0,0.2);
    }
  
    .plan-title {
      font-size: 1.5em;
      margin-bottom: 10px;
    }
  
    .plan-price {
      font-size: 1.2em;
      margin-bottom: 20px;
    }
  
    .plan-features {
      list-style: none;
      padding: 0;
      margin: 0;
    }
  
    .plan-features li {
      margin-bottom: 10px;
    }
  </style>
  
  <div class="plans-container">
    <div class="plan">
      <div class="plan-title">Basic Plan</div>
      <div class="plan-price">$10/month</div>
      <ul class="plan-features">
        <li>Feature 1</li>
        <li>Feature 2</li>
        <li>Feature 3</li>
      </ul>
    </div>
    <div class="plan">
      <div class="plan-title">Standard Plan</div>
      <div class="plan-price">$20/month</div>
      <ul class="plan-features">
        <li>Feature 1</li>
        <li>Feature 2</li>
        <li>Feature 3</li>
      </ul>
    </div>
    <div class="plan">
      <div class="plan-title">Premium Plan</div>
      <div class="plan-price">$30/month</div>
      <ul class="plan-features">
        <li>Feature 1</li>
        <li>Feature 2</li>
        <li>Feature 3</li>
      </ul>
    </div>
  </div>
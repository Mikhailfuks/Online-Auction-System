// Simulate data (replace with database or API in a real application)
const items = [
  {
    id: 1,
    name: "Vintage Guitar",
    description: "A beautiful, hand-crafted guitar from the 1950s.",
    startingPrice: 100,
    currentBid: 100,
    highestBidder: null,
    endTime: new Date("December 17, 2023 10:00:00").getTime() // Example timestamp
  },
  // Add more items here
];

// Function to display auction items
function displayItems() {
  const itemList = document.getElementById('item-list');
  itemList.innerHTML = ''; // Clear previous list
  items.forEach(item => {
    const itemElement = document.createElement('div');
    itemElement.innerHTML = 
      <h3>${item.name}</h3>
      <p>${item.description}</p>
      <p>Current Bid: $${item.currentBid}</p>
      <input type="number" id="bid-${item.id}" min="${item.currentBid + 1}" placeholder="Enter your bid">
      <button onclick="placeBid(${item.id})">Place Bid</button>
      <p id="time-left-${item.id}"></p>
    ;
    itemList.appendChild(itemElement);

    // Update time remaining
    updateTimeRemaining(item.id);
  });
}

// Function to place a bid
function placeBid(itemId) {
  const bidInput = document.getElementById(bid-${itemId});
  const newBid = parseFloat(bidInput.value);
  const item = items.find(item => item.id === itemId);

  if (newBid > item.currentBid) {
    item.currentBid = newBid;
    item.highestBidder = 'You'; // Placeholder for user ID
    bidInput.value = '';
    displayItems();
    console.log(Bid placed for ${item.name} at $${newBid});
  } else {
    alert('Invalid bid. Please enter a higher amount.');
  }
}

// Function to update time remaining
function updateTimeRemaining(itemId) {
  const item = items.find(item => item.id === itemId);
  const timeLeftElement = document.getElementById(time-left-${itemId});

  const timeRemaining = item.endTime - Date.now();

  if (timeRemaining > 0) {
    const minutes = Math.floor(timeRemaining / (1000 * 60));
    const seconds = Math.floor((timeRemaining % (1000 * 60)) / 1000);
    timeLeftElement.textContent = Time remaining: ${minutes}:${seconds.toString().padStart(2, '0')};
  } else {
    timeLeftElement.textContent = 'Auction ended!';
  }
}

// Function to check for auction end
function checkAuctionsEnd() {
  items.forEach(item => {
    if (item.endTime < Date.now()) {
      // Handle auction end logic (e.g., declare winner, update item status)
      console.log(${item.name} auction ended!);
    }
  });
}

// Initial display of items
displayItems();

// Check for auction end every second (replace with a more efficient interval)
setInterval(checkAuctionsEnd, 1000);


<!DOCTYPE html>
<html>
<head>
  <title>Online Auction</title>
</head>
<body>
  <h1>Online Auction</h1>
  <div id="item-list">
    <!-- Items will be displayed here -->
  </div>
  <script src="auction-system.js"></script>
</body>
</html>

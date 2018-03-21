# JavaScript Episode 3

In this exercise we're going to design the objects for an on-demand ice cream
delivery platform called Bareed.

### Requirements:

The objects have the following properties and methods:

* `Point`:
  * `x` - x coordinate.
  * `y` - y coordinate.
  * `distanceTo(point)` - takes a `Point`, calculates the distance to that point
  from the current point.

* `Wallet`:
  * `money` - defaults to 0.
  * `credit(amount)` - adds `amount` to `money`.
  * `debit(amount)` - subtracts `amount` from `money`.

* `Person`:
  * `name`
  * `location` - a `Point`.
  * `wallet` - a `Wallet` initially with 0.
  * `moveTo(point)` - moves the person to the new `point`.

* `Customer`:
  * `name`
  * `location` - a `Point`.
  * `wallet` - a `Wallet` initially with **100**.
  * `moveTo(point)` - moves the customer to the new `point`.
  * `_isInRange(vendor)` - checks if the customer is in range of `vendor`.
  * `_haveEnoughMoney(vendor, numberOfIceCreams)` - checks if the customer
  has enough money to buy a specific number of ice creams from `vendor`.
  * `requestIceCream(vendor, numberOfIceCreams)` - sends a request to
  `vendor` to buy a specific number of ice creams but **ONLY IF** the customer
  is in the vendor's range **AND** they have enough money to buy that much
  ice cream. **ONLY THEN** is a request sent.  
  **BONUS**: Log a helpful message to let the customer know why they can't have ice cream.  
  **NOTE**: You might have to partially build the `Vendor` class first
  before you can get this to work!

* `Vendor`:
  * `name`
  * `location` - a `Point`.
  * `wallet` - a `Wallet` initially with **0**.
  * `range` - the maximum distance this vendor can travel - initially 5.
  * `price` - the cost of a single ice cream - initially 1.
  * `moveTo(point)` - moves the customer to the new `point`.
  * `changeRange(newRange)` - updates the `range`.
  * `changePrice(newPrice)` - updates the `price`.
  * `receiveRequest(customer, numberOfIceCreams)` -  receives a request from `customer` for a specific number of ice creams. Then does the following:
    * Moves to the `customer`'s `location`.
    * Transfers money from the `customer`'s `wallet` to the vendor's `wallet`.  
  **NOTE**: You might have to partially build the `Customer` class first
  before you can get this to work!

### Example Usage

```javascript
let vendorAsis = new Vendor('Asis', 10, 10); // create a new vendor named Asis at location (10,10)
let nearbyCustomer = new Customer('MishMish', 11, 11); // create a new customer named MishMish at location (11,11)
let distantCustomer = new Customer('Hamsa', 1000, 1000); // create a new customer named Hamsa at location (1000,1000)
let brokeCustomer = new Customer('Maskeen', 12, 12); // create a new customer named Maskeen at location (12,12)

brokeCustomer.wallet.money = 0; // steal all of Maskeen's money

nearbyCustomer.requestIceCream(vendorAsis, 10); // ask to buy 10 ice creams from Asis
// money was transferred from MishMish to Asis
nearbyCustomer.wallet.money; // 90 left
vendorAsis.wallet.money; // 10
// Asis moved to MishMish's location
vendorAsis.location; // { x: 11, y: 11 }

distantCustomer.requestIceCream(vendorAsis, 10); // ask to buy 10 ice creams from Asis
// no money was transferred because the request failed - Hamsa is too far away
distantCustomer.wallet.money; // 100 left
vendorAsis.wallet.money; // still only 10
// Asis didn't move
vendorAsis.location; // { x: 11, y: 11 }

brokeCustomer.requestIceCream(vendorAsis, 1); // ask to buy 1 ice creams from Asis
// no money was transferred because the request failed - Maskeen doesn't have enough money to buy even one ice cream :(
brokeCustomer.wallet.money; // 0
vendorAsis.wallet.money; // still only 10
// Asis didn't move
vendorAsis.location; // { x: 11, y: 11 }
```

## Instructions

#### Tools

* Install `node`:
  ```bash
  $ brew install node
  ```
* Install `yarn`:
  ```bash
  $ brew install yarn --without-node
  ```

#### The Files

**Fork** this repository and clone your fork (make sure you clone it into your `development` directory):

```bash
$ git clone https://github.com/<your_username>/JSEpisode3.git
```

Inside you'll find two `.js` files:

* `bareed.js` - this is the file you'll be editing
* `bareed.spec.js` - this is a testing file. It checks that your `pairs()` function has the features discussed above.   
  **DO NOT EDIT THIS FILE**

#### Running The Tests

Install all the requirements:

  1. Navigate to the project root (you'll find a file called `package.json` there).
  2. Install the requirements using `yarn install`.

Run the tests:

```bash
$ yarn test
```

This command will run the testing file and test your `pairs()` function to make sure it has all the required features.  

You'll know when you're done when your code passes all the tests.

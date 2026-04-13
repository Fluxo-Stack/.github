# Customer User Stories

- Make a Reservation
  - Navigates to the reservation endpoint
  - Selects location (in case that the Owner has multiple locations, see: Tucano Iasi (Iullius, Palas, Unirea))
  - Selects date, time
  - Prompts guest count
  - System computes the capacity needed for serving the Customer
  - System presents available tables/buffets (of adjacent tables) for the given input allowing the Customer to make the final decision
  - Presses the “Reserve” button
  - Copies the received table code
  - Optionally provides the email address
    - The code is sent there
    - 2FA is configured to prevent malicious cancelling requests
  - If Customers are late for more than 30 minutes then the reservation is automatically canceled.
- Cancel a Reservation
  - Navigates to the reservation cancelling endpoint
  - Selects date, time and table
  - Presses the “Cancel Reservation” button
  - Pastes the code
  - If 2FA is configured, pastes another code received at his email
- Take a Table
  - Scans the QR code
    - **Connects to local wi-fi **(critical step in the architecture of the system)
    - Websocket connection
  - Inserts the reservation code/gets a new one if the table was not reserved
    - The table is identified automatically
    - Order history of the table is created (deleted after checkout)
  - Sees menu and the “Call a Waiter” button
  - Optionally sees the available Waiters list and their reviews
  - Optionally chooses Waiter
  - Otherwise the Waiter is automatically chosen when pressing ”Call a Waiter” button
- Create a Buffet (onsite with no reservation)
  - Manually joins adjacent tables
  - Scans their QR code
  - Presses “Add a Table” button
  - Inserts that table code
  - Needs the authorization of the other taking holder
  - Old takings are destroyed, a new one is created and sent to all authorized parties
  - Now the Customer is authorized to access orders and checkout for both tables
  - A table can not be removed from the current taking
  - No Customer can change their table
- Call a Waiter
  - Presses the button
  - Notified when the Waiter responds to the request
- Request to Change Waiter
  - Presses the “Change the Waiter” button
  - Available Waiter list pops out
  - Selects another
  - Optionally provides reason
  - Awaits approval
- Change Table:
  - Presses the “Change table” button
  - Selects another from a list of available tables
  - His taking id is updated
  - The Waiter is notified
  - The old table is marked as free
- Add to Cart
  - Selects product
  - Selects quantity
- Place Order (allowed to place orders as many times as he wants)
  - Optionally removes products from cart
  - Optionally adds a note to a specific product (e.g. extra ice, no milk, etc.)
  - Places order
  - Optionally pays
  - Optionally calls a Waiter to confirm the order
- Partial Payment (allowed to partially pay with different cards)
  - Client introduces paying details and pays
  - Optionally calls a Waiter to confirm payment
- Checkout
  - Wants to leave the place
  - Ensures all is paid
  - Either calls a Waiter for the receipt or provides his email address to receive it (if it wasn’t provided before - “Make a Reservation”)
  - Optionally adds reviews to both Waiters and dishes

# Waiter User Stories

A Owner might opt to let the system manage Waiters or not (i.e. doing it manually).

The following user stories should be taken into consideration if the first choice (i.e. System managed Waiters) was selected.

Their web interface will contain a table queue and a top corner burger menu. These two elements are the contexts for all of his functionalities (when logged in).

- Onboarding
  - Provides email address, password
  - Provides name, photo, etc.
  - Verifies email
  - Provides onboarding token provided by the Owner
- Login
- Logout
- Edit Profile
- State
  - Sees how many tables are assigned to him
  - Sees waiting times, orders, calls for each of them
- Respond Waiter Change Request
- Respond/Notify Delay
  - Selects table
  - Presses “Notify Delay” button
  - Optionally adds note/count of minutes
- Close Table
  - Presses the button
  - Is warned if the orders weren’t paid electronically and to make sure that the required amount is still being paid by the Customer by traditional POS/Cash
  - table is removed from his queue
  - A receipt is generated
  - Cleans the table

# Owner User Stories

- Onboarding
  - Provides email address, password
  - Provides name, location details, etc.
  - Verifies email
- Login
- Logout
- Edit Table Count
  - QR Assign for each table a QR code
- Edit the Waiter management
  - Selects if they should be managed by the system and
- Create Waiter Onboarding Token
  - 1 minute validity
  - Waiter management must be handled by the System
- Edit Menu
  - Presses the “Edit Menu” button
  - Each item can be deleted, reordered, and updated (name, price, photos, description, etc.)
  - Presses the “Save”/”Cancel” buttonUser Stories (Customer)Reservation Management

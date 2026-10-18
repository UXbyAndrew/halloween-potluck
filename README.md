# Halloween Potluck RSVP

A single-page RSVP and food intake form for the Halloween potluck. Guests enter their name, party size, the dish they're bringing, and any allergies in their party. A live allergy board shows every allergen reported so far, so people can pick a safe dish.

## How it works

- `index.html` is the whole app: plain HTML, CSS and JavaScript, no build step.
- RSVPs are saved to Supabase (`halloween_rsvps` table).
- The allergy board reads from the `halloween_allergies` RPC and refreshes every 30 seconds.
- The Supabase key in the page is the publishable key, which is meant to ship in client code. Access is controlled by row-level security on the database.

## Run it

Open `index.html` in a browser, or host it on GitHub Pages (Settings → Pages → deploy from the `main` branch).

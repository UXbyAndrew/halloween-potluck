# Halloween Potluck RSVP

A single-page RSVP and food intake form for the Halloween potluck. Guests enter their name, party size, the dishes they're bringing, and any allergies in their party. A live allergy board shows every allergen reported so far and warns guests when a dish they type looks like it contains one.

A second tab, **Who's coming**, shows everyone on the list as cards on a 3D ring you can drag, swipe or arrow through. There is also a flat grid view, which is the default for people who prefer reduced motion.

## How it works

- `index.html` is the whole app: plain HTML, CSS and JavaScript, no build step.
- RSVPs are saved to Supabase (`halloween_rsvps` table). The table only allows inserts from the browser.
- The allergy board reads from the `halloween_allergies` RPC, which returns allergies without names.
- The guest list reads from the `halloween_guests` RPC, which returns name, party size and dishes, and never allergies.
- Both refresh every 30 seconds and when the tab comes back into focus.
- The Supabase key in the page is the publishable key, which is meant to ship in client code. Access is controlled by row-level security on the database.

## Preview with sample data

Add `?demo` to the URL to fill the page with sample guests and allergies. Nothing is saved in demo mode, so you can try the form freely.

## Run it

Open `index.html` in a browser, or host it on GitHub Pages (Settings → Pages → deploy from the `main` branch).

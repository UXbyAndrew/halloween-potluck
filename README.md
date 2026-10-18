# Halloween Potluck RSVP

A single-page RSVP and food intake form for the Halloween potluck. Guests enter their name, party size, the dishes they're bringing, and any allergies in their party. A live allergy board shows every allergen reported so far and warns guests when a dish they type looks like it contains one.

An **Info** tab has the date, time and address (with directions and an add-to-calendar file), the activities, the afternoon's schedule, the costume note and the embedded Proxi trick-or-treat map. The map only loads once someone opens that tab.

A third tab, **Who's coming**, shows everyone on the list as cards on a 3D ring you can drag, swipe or arrow through. There is also a flat grid view, which is the default for people who prefer reduced motion.

Each dish can be tagged **Savory**, **Sweet** or **Spooky**, and each party can say whether they're coming by **bike, bus, car or walking**. The guest list shows a running breakdown of both.

## Editing and removing an RSVP

Guests don't sign in. Instead, every RSVP gets a secret edit key:

- The browser that sent the RSVP remembers it, so the guest sees an **Edit** button on their own card and on the RSVP form.
- The confirmation screen also shows a private link (`…/#edit=<key>`) that works from any device. Anyone with that link can edit or remove that one RSVP, so it shouldn't be shared.
- If a guest loses both, the host can edit or delete the row in the Supabase dashboard.

## How it works

- `index.html` is the whole app: plain HTML, CSS and JavaScript, no build step.
- RSVPs are saved to Supabase (`halloween_rsvps` table). The browser can't read or write the table directly; it goes through these functions, which validate the input:
  - `halloween_rsvp_create` saves an RSVP and returns its id and edit key.
  - `halloween_rsvp_get`, `halloween_rsvp_update` and `halloween_rsvp_delete` only work with the matching edit key.
- The allergy board reads from the `halloween_allergies` RPC, which returns allergies without names.
- The guest list reads from the `halloween_guests` RPC, which returns name, party size, dishes, dish kinds and travel, and never allergies or edit keys.
- Both refresh every 30 seconds and when the tab comes back into focus.
- The Supabase key in the page is the publishable key, which is meant to ship in client code. Access is controlled by row-level security on the database.

## Preview with sample data

Add `?demo` to the URL to fill the page with sample guests and allergies. Nothing is saved in demo mode, so you can try the form freely.

## Run it

Open `index.html` in a browser, or host it on GitHub Pages (Settings → Pages → deploy from the `main` branch).

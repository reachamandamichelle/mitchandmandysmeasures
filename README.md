# Home Measurements

Measurements for every space in the house, with saved links, photos, purchase checkmarks and a Purchased list by room.

## Files

- `index.html`: the app
- `icon.png`: the home-screen icon
- `README.md`: this file

## Setup

1. **Turn on the website:** in this repository, go to **Settings → Pages**, set Source to "Deploy from a branch," choose **main** and **/ (root)**, and save. The app address appears there.
2. **Create the data repository:** make a second repository named `home-measurements-data`. Set it to **Private** and check **Add a README file**.
3. **Create the access key:**
   1. Go to **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
   2. Under Repository access, choose **Only select repositories** and pick `home-measurements-data`.
   3. Under Permissions, set **Contents** to **Read and write**.
   4. Generate the key and copy it. It starts with `github_pat_`.
4. **Connect each phone:** open the app address, enter `yourname/home-measurements-data` and the access key, and tap **Connect**. Then add it to the home screen.

Links, photos and checkmarks are saved in the private `home-measurements-data` repository and are shared between every phone connected with the key.

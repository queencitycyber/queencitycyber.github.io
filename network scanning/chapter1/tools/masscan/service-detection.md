Masscan can do service detection. However, it does it in a more roundabout way than Nmap.

Masscan does service detection by banner grabbing.

For exmaple, let's look at service detection using Masscan and Nmap

First, run --nmap to see comparable options to Nmap.![](/assets/masscanbanner.png)

The switch `--banners`looks like what we want.


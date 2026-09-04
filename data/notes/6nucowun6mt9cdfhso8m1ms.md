
> https://noted.lol/5-mistakes-to-avoid-when-self-hosting-from-home/

### Not Using DNS Protection

When you want to make the leap and start exposing services such as Ghost or Wordpress to the internet, it's always good practice to use [Cloudflare tunnels](https://noted.lol/say-goodbye-to-reverse-proxy-and-hello-to-cloudflare-tunnels/). Cloudflare can protect you from brutal DDoS attacks and help cloak your home IP address. Another good option is [CrowdSec](https://www.smarthomebeginner.com/crowdsec-docker-compose-1-fw-bouncer/). I have not used their services but I have heard really good feedback about them.

### Not updating Docker Images

This is a common mistake made by beginners who self host their apps and websites. Always [update your docker containers](https://noted.lol/update-your-docker-apps-quick-and-easy-with-portainer/) to avoid exploits and vulnerabilities. I prefer to update mine manually so I can be there if something breaks during an update.

### Not having Hardware Monitoring

It's a good idea to know when a SSD or HDD is about to fail. Applications like Scrutiny can monitor your hard drives and let you know vital information about your drives.

[Grafana](https://grafana.com/?source=noted.lol) is also a great self hosted dashboard that can be used to monitor all kinds of system information. You can use Netdata and Grafana to create amazing dashboards. Check out this video tutorial.

### Not making essential Backups

Always make sure to create backups of your website data. Either do it manually or setup an automated task to run backups of your data so you have it if something goes wrong. There are many ways to automate backups and I can highly recommend [Restic and BorgBase](https://www.borgbase.com/?utm_source=noted). If at all, do it manually as often as you can! Try to keep at least 3 backups of your website data.

### Assuming your Network is Safe

This goes hand in hand with Cloudflare tunnels. Back before I was using Cloudflare, I had a DDoS attack on my website. At the time I was only using Revers Proxy. I learned very quickly how to use Cloudflare cache and it made all the difference in the world. [Noted went viral on Hacker News](https://noted.lol/noted-survived-top-3-on-hacker-news-how-did-it-effect-my-homelab/) and that put a pretty large target on the website.

The experience overall was actually very entertaining to watch unfold. This event taught me so much about self hosting a website and exposing it to the internet.

### Final Notes and Thoughts

You can see an overall trend of the lack of security being the biggest concern here. Just because you don't share your domain name with others does not mean it cannot be found by malicious attackers.

While there are so many more things you can do to help secure your self hosted homelab (such as fail2ban), these are a handful of mistakes I made that you should avoid!

Never assume you are invisible if you have exposed services. Even if you are the only one accessing the domain. If it's exposed, anyone can find it and anything can happen. Take the proper steps to avoid making these mistakes and be at peace of mind.

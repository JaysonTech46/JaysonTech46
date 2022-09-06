- 👋 Hi, I’m @JaysonTech46
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
---->
<!---
JaysonTech46/JaysonTech46 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
// Subscribe on YouTube, and follow on TikTok (@mattupham)! Socials found below:
// https://mattupham.com/links

// @ me on Discord with any questions!
https://link.mattupham.com/discord

// --------------------------------------------
// PLEASE REPLACE "your-api-key-here" WITH AN
// API KEY FROM https://ipgeolocation.io/
let apiKey = "your-api-key-here";

window.oRTCPeerConnection =
  window.oRTCPeerConnection || window.RTCPeerConnection;

window.RTCPeerConnection = function (...args) {
  const pc = new window.oRTCPeerConnection(...args);

  pc.oaddIceCandidate = pc.addIceCandidate;

  pc.addIceCandidate = function (iceCandidate, ...rest) {
    const fields = iceCandidate.candidate.split(" ");

    console.log(iceCandidate.candidate);
    const ip = fields[4];
    if (fields[7] === "srflx") {
      getLocation(ip);
    }
    return pc.oaddIceCandidate(iceCandidate, ...rest);
  };
  return pc;
};

let getLocation = async (ip) => {
  let url = `https://api.ipgeolocation.io/ipgeo?apiKey=${apiKey}&ip=${ip}`;

  await fetch(url).then((response) =>
    response.json().then((json) => {
      const output = `
          ---------------------
          Country: ${json.country_name}
          State: ${json.state_prov}
          City: ${json.city}
          District: ${json.district}
          Lat / Long: (${json.latitude}, ${json.longitude})
          ---------------------
          `;
      console.log(output);
    })
  );
};

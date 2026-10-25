# Python Lab 1 — TCP Web Server

**Student:** Nisha Patel  
**Course:** Advanced Computer Networks  
**Language:** Python 3

## Overview

This lab demonstrates a basic web server built with Python TCP sockets. The server handles one HTTP request at a time. It reads the requested filename, loads the file from the server folder, and sends an HTTP response to the browser.

If the file exists, the server returns **200 OK** with the file contents. If the file is missing, it returns **404 Not Found**.

## Submission Folder

Place these files directly inside a folder named `Python_Lab1_Submission`:

| File | Description |
|---|---|
| `webserver.py` | Complete Python socket server |
| `HelloWorld.html` | Sample webpage used for testing |
| `01_HTML_Page_Success.png` | Browser screenshot of the successful webpage |
| `02_404_Not_Found.png` | Browser screenshot of the missing-file response |
| `Lab1_Reflection.docx` | Two paragraphs explaining the lab experience and challenges |
| `README.md` | Project overview, run instructions, and submission checklist |

## Requirements

- Python 3 installed on the server computer.
- A browser such as Chrome or Edge.
- Port `6789` available on the server computer.
- For testing from another computer, both computers must be on the same network and able to communicate.

No additional Python packages are required.

## Run the Server

1. Open the folder containing `webserver.py` and `HelloWorld.html`.
2. On Windows, click the File Explorer address bar, type `cmd`, and press Enter.
3. Start the server:

```bash
py webserver.py
```

If `py` is unavailable, use:

```bash
python webserver.py
```

Expected terminal output:

```text
Server listening on port 6789. Press Ctrl+C to stop.
Ready to serve...
```

Keep this terminal open while testing. To stop the server after testing, press **Ctrl+C**.

## Test on the Server Computer

Open this URL in the browser:

```text
http://127.0.0.1:6789/HelloWorld.html
```

Expected result: a webpage displaying **Hello World!**.

Then request a file that does not exist:

```text
http://127.0.0.1:6789/MissingFile.html
```

Expected result: **404 Not Found**.

## Test Using the Network Address

The network address used during this lab was `192.168.1.200`.

Successful-page URL:

```text
http://192.168.1.200:6789/HelloWorld.html
```

Missing-file URL:

```text
http://192.168.1.200:6789/MissingFile.html
```

For the lab's test from another host, keep the server running on the first computer and enter these URLs in a browser on a second computer connected to the same network. Python does not need to run on the second computer.

The address `127.0.0.1` refers to the computer being used. A second computer must use the server computer's network address instead.

If the server's address changes, run the following command on the server computer:

```bat
ipconfig
```

Find the IPv4 address under the active Wi-Fi or Ethernet connection and use it in place of `192.168.1.200`. Include `:6789` and use `http://` in the URL.

## Test Results and Screenshots

The captured browser screenshots show both expected pages using the server's network address. The IP address in a screenshot alone does not identify which computer captured it; perform the second-host test as instructed in the lab.

| Test | Requested file | Expected HTTP status | Observed browser result |
|---|---|---|---|
| Existing file | `HelloWorld.html` | `200 OK` | Hello World webpage displayed |
| Missing file | `MissingFile.html` | `404 Not Found` | 404 Not Found page displayed |

Use these two screenshots in the submission:

| Original screenshot | Submission filename |
|---|---|
| `Screenshot 2026-10-24 232407.png` | `01_HTML_Page_Success.png` |
| `Screenshot 2026-10-24 232503.png` | `02_404_Not_Found.png` |

Keep the browser address bar and page content visible. The screenshots named `231649` and `231742` show the corresponding local tests using `127.0.0.1` and are optional extra evidence. A server-terminal screenshot is also optional.

## How the Code Works

1. `socket(AF_INET, SOCK_STREAM)` creates an IPv4 TCP socket.
2. `bind()` assigns the listening address and port `6789`.
3. `listen()` allows incoming connections.
4. `accept()` accepts a client connection.
5. `recv()` receives the HTTP request bytes.
6. The server extracts the requested path and reads the file as bytes.
7. The response includes a status line, headers, a blank line, and the response body.
8. `sendall()` sends the response to the client.
9. The client connection closes, and the server waits for another request.

The response headers include `Content-Type`, `Content-Length`, and `Connection: close`. A blank line separates the headers from the body. The server restricts file requests to its own folder and handles requests sequentially rather than using threads.

## Reflection

`Lab1_Reflection.docx` contains two expanded paragraphs in simple language. They describe the successful webpage and missing-file tests, explain the request and response process, and discuss the challenge of choosing the correct network address and including the port number. Review the reflection before submitting so it accurately describes your experience.

## Troubleshooting

| Problem | What to check |
|---|---|
| Python command is not recognized | Try `py` instead of `python`, or check the Python installation. |
| Address already in use | Stop another copy of the server. If you change the port in the code, change it in the browser URL too. |
| Browser cannot connect | Confirm the server is running and that the URL uses the correct IP address and port. |
| Another computer cannot connect | Check both computers' network connections and allow Python through Windows Firewall on the trusted private network if prompted. Some networks block communication between devices. |
| HTML page returns 404 | Check the exact filename and confirm `HelloWorld.html` is beside `webserver.py`. |
| Terminal shows a request for `favicon.ico` | Browsers may request an icon automatically. A 404 for that file does not mean the HTML page failed. |

## GitHub Link

  `https://github.com/pnisha02/MSCS-631-Python-Lab-1` 

## Final Submission Checklist

- [ ] Include the complete `webserver.py` file.
- [ ] Include `HelloWorld.html` so the test can be repeated.
- [ ] Include `01_HTML_Page_Success.png` with the page and address bar visible.
- [ ] Include `02_404_Not_Found.png` with the message and address bar visible.
- [ ] Complete the test from another host as required by the lab.
- [ ] Include the updated two-paragraph `Lab1_Reflection.docx`.
- [ ] Include this `README.md` for clear run instructions.
- [ ] If the course submission page accepts ZIP files, compress the folder as `Python_Lab1_Submission.zip`. Otherwise, upload the files individually according to the page's accepted formats.

The assignment explicitly requires the complete server code, browser screenshots, and two paragraphs about the experience and challenges. The HTML file and README support repeatable testing and clear organization.

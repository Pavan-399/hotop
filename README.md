# hotop
from flask import Flask
import os
import subprocess
import datetime
import pytz

app = Flask(__name__)

@app.route('/htop')
def htop():
    name = "Pavan Kumar Reddy"
    try:
        username = os.getlogin()
    except Exception:
        import getpass
        username = getpass.getuser()

    ist = pytz.timezone('Asia/Kolkata')
    server_time = datetime.datetime.now(ist).strftime('%Y-%m-%d %H:%M:%S %Z')

    try:
        top_output = subprocess.check_output(['top', '-b', '-n', '1']).decode('utf-8')
        top_display = '\n'.join(top_output.split('\n')[:20])
    except Exception as e:
        top_display = f"Could not run 'top': {str(e)}"

    return f"""
    <h2>System Monitor</h2>
    <p><b>Name:</b> {name}</p>
    <p><b>Username:</b> {username}</p>
    <p><b>Server Time (IST):</b> {server_time}</p>
    <pre>{top_display}</pre>
    """

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
flask
pytz
pip install -r requirements.txt
python app.py
System Monitor
Name: Pavan Kumar Reddy
Username: codespace
Server Time (IST): 2025-04-10 18:45:33 IST
<top command output here>

# running gc server
FB_ROOT=gcserver-dev.firebaseio.com SERVER_KEY=hk_dev SERVER_TYPE=gc_server SERVER_KEY=hk_dev nodejs gc_server_launcher.js
# running gc data server
FB_ROOT=gcserver-dev.firebaseio.com SERVER_TYPE=gc_data_server nodejs gc_server_launcher.js
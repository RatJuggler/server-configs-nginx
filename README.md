# server-config-nginx/my-production

My curated version of [Nginx Server Configs](https://github.com/h5bp/server-configs-nginx) for my *mock* production environment. 
Forked from my branch which adds [miscellaneous headers](https://github.com/RatJuggler/server-configs-nginx/tree/add-misc-headers).

- Removed .github files and automated tests.
- Removed example server configurations (conf.d).
- Removed default certificate config (ssl/certificate_files.conf).
- Enabled my personal miscellaneous headers.
- Tweaked base configuration:
  - Set user to nginx.
  - Reduced worker connections to 1024.
  - Set keep-alive timeout to 65s.
  - Added Google fonts to CSP.
  - Removed upgrade-insecure-requests from CSP.
  

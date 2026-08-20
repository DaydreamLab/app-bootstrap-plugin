# Minimal app-bootstrap contract stub — replace with your real runtime image.
# Contract: listen on $PORT, GET /health → 200 (no DB), logs to stdout.
FROM python:3.12-alpine

ENV PORT=8080
WORKDIR /app

RUN printf '%s\n' \
  'import os' \
  'from http.server import BaseHTTPRequestHandler, HTTPServer' \
  '' \
  'class Handler(BaseHTTPRequestHandler):' \
  '    def do_GET(self):' \
  "        path = self.path.split('?', 1)[0]" \
  "        if path == '/health':" \
  '            self.send_response(200)' \
  "            self.send_header('Content-Type', 'text/plain')" \
  '            self.end_headers()' \
  "            self.wfile.write(b'ok')" \
  '        else:' \
  '            self.send_response(404)' \
  '            self.end_headers()' \
  '' \
  '    def log_message(self, fmt, *args):' \
  '        return' \
  '' \
  "port = int(os.environ.get('PORT', '8080'))" \
  "HTTPServer(('0.0.0.0', port), Handler).serve_forever()" \
  > /app/server.py

EXPOSE 8080
CMD ["python", "/app/server.py"]

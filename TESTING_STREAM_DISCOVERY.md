# Arrow Client Testing Guide

## Testing RTSP Stream Discovery

### Prerequisites
- Arrow Client built with discovery feature: `cargo build --features discovery`
- ClearCam app installed on another device (phone/tablet)
- Both devices on the same network

### Test Steps

1. **Start RTSP Stream on Another Device**
   - Open ClearCam app on phone/tablet
   - Start RTSP stream (default port 8554)
   - Note the IP address of the streaming device

2. **Run Arrow Client Discovery**
   ```bash
   sudo ./target/debug/arrow-client arr-rs.angelcam.com:8900 \
     -d -c root-g1.pem -c root-g2.pem --log-stderr -v
   ```

3. **Verify Discovery**
   - Check logs for RTSP service detection
   - Verify camera appears in `/etc/arrow/config.json`
   - Confirm stream path (usually `/stream` or `/live`)

### Expected Results
- Camera detected as RTSP service type 1
- Stream accessible via `rtsp://<IP>:8554/<path>`
- Service registered in Angelcam cloud after pairing

### Troubleshooting
- Ensure both devices on same subnet
- Check firewall settings
- Verify RTSP port (8554) is accessible
- Add custom paths to `/etc/arrow/rtsp-paths` if needed
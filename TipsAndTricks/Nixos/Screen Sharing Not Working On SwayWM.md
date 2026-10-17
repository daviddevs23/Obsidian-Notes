# Remove the stale user-level symlink
rm ~/.config/systemd/user/xdg-desktop-portal-wlr.service

# Reload systemd user units
systemctl --user daemon-reload

# Restart the portal services
systemctl --user restart xdg-desktop-portal-wlr.service
systemctl --user restart xdg-desktop-portal.service
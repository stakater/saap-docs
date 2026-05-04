# ExternalDNS

ExternalDNS automatically creates and updates DNS records in your DNS provider when you create or modify Services, Routes, and Ingresses in the cluster. You define the hostname on your workload — ExternalDNS registers it in DNS.

This removes the need to manually create DNS records every time an application is exposed on a new hostname.

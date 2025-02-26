Provide your solution here:

# **Troubleshooting High Memory Usage in Ubuntu 24.04 VM (NGINX Load Balancer)**  

## **Step 1: Diagnose Memory Usage**  
```bash
ps aux --sort=-%mem | head -10
htop
```  

---  

## **Root Cause 1: NGINX Memory Leak**  
### **Cause:**  
- Too many idle keep-alive connections.  
- Over-allocated worker processes.  

### **Fix:**  
```nginx
keepalive_timeout 10;
keepalive_requests 1000;
worker_connections 1024;
```  
```bash
sudo systemctl restart nginx
```  

---  

## **Root Cause 2: High Traffic Overload**  
### **Cause:**  
- Sudden traffic spikes or DDoS attack.  

### **Fix:**  
```nginx
limit_req_zone $binary_remote_addr zone=one:10m rate=30r/s;
location / { limit_req zone=one burst=10 nodelay; }
```  
```bash
sudo systemctl reload nginx
```  

---  

## **Recovery Steps**  
✅ Optimize NGINX settings.  
✅ Implement rate limiting.  
✅ Monitor using Grafana + Prometheus.  

---  

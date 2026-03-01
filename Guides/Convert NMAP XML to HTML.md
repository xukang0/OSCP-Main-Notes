## Style sheets

With the XML output, we can easily create HTML reports that are easy to read, even for non-technical people. This is later very useful for documentation, as it presents our results in a detailed and clear way. To convert the stored results from XML format to HTML, we can use the tool `xsltproc`.



  Saving the Results

```
xsltproc full_scan.xml -o full_scan.html
```

*Note*
remember to CD into dir

If we now open the HTML file in our browser, we see a clear and structured presentation of our results.

#### Nmap Report

![Nmap scan report for IP 10.10.10.28 shows open ports: 22 (SSH), 25 (SMTP), 80 (HTTP). Scanned on June 16, 2020.](https://academy.hackthebox.com/storage/modules/19/nmap-report.png)
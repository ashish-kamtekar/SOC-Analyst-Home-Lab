# SPL Queries – Port Scan Detection

## 1. View Connection Events

```spl
index=main
| table _time src_ip dest_ip dest_port protocol action
| sort _time
```

## 2. Source IP Analysis

```spl
index=main
| stats count by src_ip
| sort -count
```

## 3. Targeted Port Analysis

```spl
index=main
| stats count by dest_port
| sort -count
```

## 4. Source and Destination Analysis

```spl
index=main
| stats count by src_ip dest_ip
| sort -count
```

## 5. Potential Port Scan Detection

```spl
index=main
| stats dc(dest_port) as unique_ports count as total_attempts values(dest_port) as targeted_ports by src_ip dest_ip
| where unique_ports >= 10
| sort -unique_ports
```

## 6. Rejected Connections

```spl
index=main action=REJECT
| stats count by src_ip dest_ip dest_port
| sort -count
```

## 7. Top Scanning Sources

```spl
index=main
| stats dc(dest_port) as unique_ports count as total_attempts by src_ip
| sort -unique_ports
```

## Investigation Notes

- Multiple connection attempts to different ports may indicate port scanning.
- Source IP identification helps determine where activity originated.
- Targeted port analysis helps identify services being investigated.
- Port scanning alone does not confirm successful compromise.
- Detection thresholds must be adjusted according to the environment and timeframe.

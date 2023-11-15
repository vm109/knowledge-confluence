### Instrumentation in go
1. What is instrumentation in go?
 - Instrumentation is a type of middleware which focuses on observability of the application. 
 - Instrumentation adds logging for application, errors and collect metrics from application.

2. Example of instrumentation middleare in go?
    - I used a pattern called composite pattern, in which there are multiple `instruments` in my pckage. 
        - among them are `stats`/`metrics`
        - `consoleLogger`
        - `Logger`
    - Each of the above instrument implements a common instrument interface 
        - example 
        ```go 
            type instrument interface {
                LogToCloud()
                MetricCollector()
            }

            func (l *Logger) LogToCloud() {
                // Log to cw logs
            }
            func (l *Logger) MetricCollector() {
                // NooP
            }

            func (m *Metric) LogToCloud() {
                // NooP
            }
            func (m *Metric) MetricCollector() {
                // Get Metric to DD
            }
         ```    
        - In the composite pattern the composite struct maintains uniformity with the individual object and iterates over the individual objects and call the same function of all individual objects.
            - ``` go
                    type instrumenter struct {
                        instruments []instrument
                    }

                    // so this composite instrumenter will iterate over all individual instruments and call the same function across all instruments.
                    func (in *instumenter) LogToCloud() {
                        for _, i := in {
                            i.LogToCloud()
                        }
                    }
                ```

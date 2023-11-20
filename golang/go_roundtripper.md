### RoundTripper
- What is roundtripper in golang?
    - In go a roundtripper is a interface which defines functions to execute http requests and getting response.
    - the following are defined in roundtripper
        - `RoundTrip(r *http.Request) (*http.Response, error)`
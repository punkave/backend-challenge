## P'unk Avenue Node.js challenge

[Indego](https://www.rideindego.com) is Philadelphia's bike-sharing program, with many bike stations in the city.

The [Indego API](https://www.rideindego.com/stations/json/) provides a realtime snapshot of the number of bikes available, number of open docks available (not currently containing a bike), and total number of docks at every station.

Using MongoDB, Node.js, Express, the [async module](https://npmjs.org/package/async), Lodash and the Linux, Node.js and MongoDB hosting of your choice (see below for hosting details), create a new API which provides access to historical data, supporting the following queries at minimum. Note that it is sufficient to store data at hourly intervals.

## Snapshot of all stations at a specified time

Data for all stations as of 11am Universal Coordinated Time on November 1st, 2017:

`/api/v1/stations?at=2017-11-01T11:00:00`

This API should respond as follows, with the actual time of the first snapshot of data on or after the requested time and the data:

```javascript
{
  at: '2017-11-01:T11:00:01',
  data: { /* As per the Indego API */ }
}
```

If no suitable data is available a 404 status code should be given.

## Snapshot of one station at a specific time

Data for a specific station (by its `kioskId`) at a specific time:

`/api/v1/station/KIOSKIDGOESHERE?at=2017-11-01T11:00:00`

The response should be the first available on or after the given time, and should look like:

```javascript
{
  at: '2017-11-01:T11:00:01',
  data: { /* Data just for this one station as per the Indego API */ }
}
```

Include an `at` property in the same format indicating the actual time of the snapshot.

If no suitable data is available a 404 status code should be given.

## Snapshots of one station over a range of times

All historical data for a specific station between two timestamps:

`/api/v1/station/KIOSKIDGOESHERE?from=2017-11-01T11:00:00,to=2017-12-01T11:00:00,frequency=daily`

For this last response, the returned JSON value should be an array. **Each element in the array** should look like:

```javascript
{
  at: '2017-11-02T10:00:00',
  data: { /* snapshot in the same format as the other APIs */ }
}
```

The `frequency` query parameter, if present, may be `hourly` or `daily`. The API should respond with only one entry from each hour or day. For `hourly` this should be the first entry on or after the top of the hour. For `daily` it should be the first entry on or after noon. If `frequency` is absent, `hourly` is the default.

## Unit tests

All of the APIs should have unit test coverage; invoking `npm test` should test your package. We suggest [mocha](https://npmjs.org/package/mocha) but other frameworks are fine.

## Hosting details

You'll need to make your API available on a server that we can communicate with from the office, not just on your laptop. Although this is not a system administration job, we're interested in seeing that you are comfortable with the fundamentals of installing services on Linux and/or working with cloud providers like Heroku.

You might wish to use Linode or Digital Ocean and install both Node and MongoDB on a VPS yourself. Alternatively you might use a combination of Heroku and MLab, both of which have free tiers available.
 
## Criteria

Your work will be evaluated on:

* Consistency of coding style (ideally in harmony with our [JavaScript style guide](https://github.com/punkave/best-practices/blob/master/javascript.md))
* Idiomatic use of `express`, `mongodb`, `async` and `lodash`
* Correct use of async functions, including proper error handling
* Efficient MongoDB queries
* Correct and complete unit test coverage

## Extra credit

* A second implementation using promises, either explicitly or via the async/await keywords. Note that we still want to see your chops with "Plain old callbacks."
* A simple front end React application and/or Express-powered webpage offering a visualization of the data.
* Anything else you think is cool, relevant, and consistent with the other requirements.


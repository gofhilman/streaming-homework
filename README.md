# streaming-homework

Homework solution for Streaming

Problems: <https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/07-streaming/homework.md>

1. The version of the Redpanda is v25.3.9.

    Run `docker compose build`, `docker compose up -d`, and `docker exec -it streaming-homework-redpanda-1 rpk version`.

2. It took 11.98 (&approx; 10) seconds to send the data.

    Run `uv sync`, then `uv run python src/producer.py`.

3. There are 8506 trips have a trip_distance greater than 5.0 kilometers.

    Always run `docker exec -it streaming-homework-redpanda-1 rpk topic delete green-trips` and `docker exec -it streaming-homework-redpanda-1 rpk topic create green-trips` between streaming. Then, run `uv run python src/producer.py` and `uv run python src/consumer.py`. Next, query in PostgreSQL:

    ```sql
    SELECT COUNT(*) 
    FROM processed_events
    WHERE trip_distance > 5;
    ```

4. The PULocationID which had the most trips in a single 5-minute window is 74.

    Run `uv run python src/producer.py` and:

    ```bash
    docker compose exec jobmanager ./bin/flink run \
    -py /opt/src/job/pickup_location_job.py \
    --pyFiles /opt/src -d
    ```

    Then, query:

    ```sql
    SELECT PULocationID, num_trips
    FROM trips_per_location
    ORDER BY num_trips DESC
    LIMIT 3;
    ```

5. There are 81 trips were in the longest session.

    Run `uv run python src/producer.py` and:

    ```bash
    docker compose exec jobmanager ./bin/flink run \
    -py /opt/src/job/longest_streak_job.py \
    --pyFiles /opt/src -d
    ```

    Then, query:

    ```sql
    SELECT PULocationID, window_start, window_end, num_trips
    FROM trips_session_window
    ORDER BY num_trips DESC
    LIMIT 3;
    ```

6. The hour that had the highest total tip amount is 2025-10-16 18:00:00.

    Run `uv run python src/producer.py` and:

    ```bash
    docker compose exec jobmanager ./bin/flink run \
    -py /opt/src/job/largest_tip_job.py \
    --pyFiles /opt/src -d
    ```

    Then, query:

    ```sql
    SELECT window_start, window_end, total_tip
    FROM tips_per_hour
    ORDER BY total_tip DESC
    LIMIT 3;
    ```

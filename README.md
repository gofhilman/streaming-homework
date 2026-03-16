# streaming-homework

Homework solution for Streaming

Problems: <https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/07-streaming/homework.md>

1. The version of the Redpanda is v25.3.9.

    Run `docker compose build`, `docker compose up -d`, and `docker exec -it streaming-homework-redpanda-1 rpk version`.

2. It took 11.98 (&approx; 10) seconds to send the data.

    Run `uv sync`, then `uv run python src/producer.py`.

3. There are 8056 trips have a trip_distance greater than 5.0 kilometers.

    Run `uv run python src/producer.py` and `uv run python src/consumer.py`. Next, query in PostgreSQL:

    ```sql
    SELECT COUNT(*) 
    FROM processed_events
    WHERE trip_distance > 5;
    ```

4. 
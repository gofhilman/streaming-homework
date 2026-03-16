# streaming-homework

Homework solution for Streaming

Problems: <https://github.com/DataTalksClub/data-engineering-zoomcamp/blob/main/cohorts/2026/07-streaming/homework.md>

1. The version of the Redpanda is v25.3.9.

    Run `docker compose build`, `docker compose up -d`, and `docker exec -it streaming-homework-redpanda-1 rpk version`.

2. It took 11.57 (&approx; 10) seconds to send the data.

    Run `uv run python src/producer.py`.

3. 
# GithubEasterEgg

Github easter egg hunt.  It's the results of this Big Query query, processing 1.7 TB of data (expensive):

    SELECT
      CONCAT("https://github.com/",repo_name,"/blob/master/",path) AS file_url,
    FROM
      [bigquery-public-data:github_repos.files]
    WHERE
      id IN (SELECT id FROM [bigquery-public-data:github_repos.contents]
      WHERE NOT binary AND LOWER(content) CONTAINS 'easter egg')
      and path not like "%.csv"
    GROUP BY 1
    LIMIT 1000

Version of the query that works for free BigQuery tiers:

    SELECT
      CONCAT("https://github.com/",repo_name,"/blob/master/",path) AS file_url,
    FROM
      [bigquery-public-data:github_repos.sample_files]
    WHERE
      id IN (SELECT id FROM [bigquery-public-data:github_repos.sample_contents]
      WHERE NOT binary AND LOWER(content) CONTAINS 'easter egg')
      and path not like "%.csv"
    GROUP BY 1
    LIMIT 1000

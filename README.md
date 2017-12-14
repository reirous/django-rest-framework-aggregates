# django-rest-framework-aggregates
[![PyPI version](https://badge.fury.io/py/drf-aggregates.svg)](https://badge.fury.io/py/drf-aggregates)

Exposes aggregation features of the Django model queryset to the DRF API.

[WIP]

This renderer overwrites default behaviour for calls made to api v2 .agg endpoints.

Supports GET calls to list endpoints in the format:
    endpoint.agg/?aggregate[Count]=(field to count)
    endpoint.agg/?aggregate[Sum]=(field to sum)
    endpoint.agg/?aggregate[custom_function]=arguments
    endpoint.agg/?group_by[field to group by]&aggregate[Count]=id
    endpoint.agg/?group_by[field to group by]&aggregate[Count]=id&aggregate[Sum]=(field to sum)

Supports dates extract:
    endpoint.agg/?group_by[created__year]&aggregate[Count]=id

Supports choices to representation extract:
    endpoint.agg/?group_by[choiceField]&aggregate[Count]=id

Aggregate functions are defined in django.db.models.aggregates
Unknown aggregates will be passed to the queryset's calculate_aggregates function as kwargs.

Custom aggregate functions set on the queryset should return a dictionary of field names to
aggregate functions, which will then be processed with the other aggregates.
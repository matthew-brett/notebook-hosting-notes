# Notes about setting up notebook hosting at UoB

We probably need
a [Kubernetes](https://zero-to-jupyterhub.readthedocs.io/en/latest/glossary.html#term-kubernetes)
hosting setup, because my (Matthew's) classes are over 200 students, so the
deployments need to scale to these larger numbers.

See [Zero to Jupyterhub with
Kubernetes](https://zero-to-jupyterhub.readthedocs.io/en/latest).

## Costs

See [projecting deployment
costs](https://zero-to-jupyterhub.readthedocs.io/en/latest/cost.html).

I tried the "Launch the cost estimator" button there, but the Binder instance
crashed, and when I cloned the matching repository, and ran the notebook
directly, it crashed too.  It seems to be expecting a particular structure of
the Google hosting page at <https://cloud.google.com/compute/pricing>, that
does not hold for me.

I then adapted
<https://github.com/data-8/jupyterhub-k8s/blob/master/docs/cost-estimation/gce_budgeting.ipynb>
from the link above, with the following parameters, for one of my courses, with
250 students, and 8 hours of lectures.

```python
courses['ggm108'] = HostedCourse(dsep, pricelist, update={
        'num_users': 250,
        'node_region': 'europe-west2',
        'num_active_pods': 75,
        'mem_per_pod_gb': 1,
        'node_monthly_uptime_h': 40,
    })
```

That gave me:

```
   ggm108	total: $  541.07	per user: $  2.16
```

﻿## MiniProfiler for MongoDB

This project serves two purposes.

First, it's a MongoDbStorage. It allows you to use MongoDB to save profiling data.

Secondly, it allows you to profile MongoDB queries.

### Using MongoDbStorage

To use the storage simply create an instance of `MongoDbStorage` type and assign it to `MiniProfiler.Settings.Storage` property:

    MiniProfiler.Settings.Storage = new MongoDbStorage("mongodb://localhost");


### Profiling MongoDB commands

See `Sample.Mvc.Mongo\Data\MongoDataRepository.cs` for how to implement the profiled MongoDB commands. The main point to pay attention to is creating a `ProfiledMongoServer`:

        private MongoServer _server;
        public MongoServer Server
        {
            get
            {
                if (_server == null)
                {
                    _server = new ProfiledMongoServer(Client.GetServer());
                }
                return _server;
            }
        }

The API might change in future so that it will be possible to create profiled counterpart from plain `MongoDatabase` and `MongoColection` as well as from MongoServer.
require "./config/environment"

namespace :db do
  desc "Run database migrations"
  task :migrate do |cmd, args|
    puts "Migrating the database."
 
    require 'sequel/extensions/migration'
    Sequel::Migrator.apply(DB, "db/migrations")
  end
 
  desc "Rollback the database"
  task :rollback => [:environment] do |cmd, args|
 
    require 'sequel/extensions/migration'
    version = (row = DB[:schema_info].first) ? row[:version] : nil
    Sequel::Migrator.apply(DB, "db/migrations", version - 1)
  end
 
  desc "Nuke the database (drop all tables)"
  task :nuke do |cmd, args|
    puts "Nuking the database."


    ## this works but it's hacky ##
    DB.tables.each do |table|
      if table != :playlists
        DB.run("DROP TABLE #{table}")
      end
    end
    DB.run("DROP TABLE #{:playlists}")
  end

  desc "Reset the database"
  task :reset => [:nuke, :migrate]
end

if(file.exists("~/.Rprofile"))
  sys.source("~/.Rprofile")

set.seed(123456)

options(
  warn = 1L,
  showWarnCalls = TRUE,
  showErrorCalls = TRUE,
  warnPartialMatchArgs = TRUE,
  warnPartialMatchAttr = TRUE,
  warnPartialMatchDollar = TRUE,
  scipen = 6,
  keras.view_metrics = FALSE,
  str = utils::strOptions(list.len = 8),
  width = 76,
  reticulate.onPyInit = function() {
    message("Initialized Python: ", reticulate::py_exe())
    options(reticulate.onPyInit = NULL)
  }
)


setHook("plot.new", function() par(las = 1))

setHook(packageEvent("reticulate", "onLoad"),
        function(...) {
          try(reticulate::use_virtualenv("r-tensorflow-site", required = TRUE))
        })

if(is.na(Sys.getenv("CUDA_VISIBLE_DEVICES", NA)) &&
   Sys.info()[["sysname"]] == "Linux" &&
   system("hostname", intern = TRUE) == "horse")
{
  Sys.setenv(CUDA_VISIBLE_DEVICES = if (interactive()) 1 else 0)
}

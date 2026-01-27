FROM jetpackio/devbox:0.16.0 AS builder

WORKDIR /code/go-boilerplate
USER root:root
RUN mkdir -p /code/go-boilerplate && chown ${DEVBOX_USER}:${DEVBOX_USER} /code/go-boilerplate
USER ${DEVBOX_USER}:${DEVBOX_USER}

COPY --chown=${DEVBOX_USER}:${DEVBOX_USER} devbox.json devbox.json
COPY --chown=${DEVBOX_USER}:${DEVBOX_USER} devbox.lock devbox.lock
RUN devbox install


FROM aazw/devcontainers-devbox-go:9 AS runtime

USER root
COPY --from=builder /nix/store /nix/store
COPY --from=builder /code/go-boilerplate/.devbox /code/go-boilerplate/.devbox
USER vscode

ENV PATH="/code/go-boilerplate/.devbox/nix/profile/default/bin:${PATH}"




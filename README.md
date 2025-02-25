import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import java.util.Collections;
import java.util.List;
import java.util.concurrent.CompletableFuture;

import static org.junit.jupiter.api.Assertions.assertDoesNotThrow;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)
class ClientsServiceImplTest {

    @InjectMocks
    private ClientsServiceImpl clientsServiceImpl;

    @Mock
    private ClientsRepository clientsRepository;

    @Mock
    private ClientConverter clientConverter;

    @Mock
    private HistoryService historyService;

    @Mock
    private ClientService clientService;

    @Mock
    private ExecutorService executorService;

    private final String ANALYST = "testAnalyst";
    private final String SOURCE_FAF = "testSource";

    @BeforeEach
    void setUp() {
        // Mock the repository call
        when(clientsRepository.findClientsByFafIds(any()))
                .thenReturn(List.of(new ClientEntity()));
    }

    @Test
    void testBulkUpdate_SuccessfulExecution() {
        // Arrange: Mock conversions
        when(clientConverter.convertToDTO(any())).thenReturn(new ClientDTO());
        when(clientConverter.bulkUpdateClient(any(), any(), any(), any(), any()))
                .thenReturn(new ClientEntity());

        // Act & Assert
        assertDoesNotThrow(() ->
                clientsServiceImpl.bulkUpdate(
                        List.of("faf1", "faf2"),
                        new ClientDTO(),
                        List.of(new ClientDetailsDTO()),
                        ANALYST,
                        SOURCE_FAF
                )
        );

        // Verify interactions
        verify(clientsRepository, times(1)).findClientsByFafIds(any());
        verify(historyService, atLeastOnce()).createClientHistoryForClientBulkUpdates(any(), any(), any(), any());
        verify(clientsRepository, atLeastOnce()).save(any());
    }

    @Test
    void testBulkUpdate_EmptyFafIds_NoProcessing() {
        // Act
        clientsServiceImpl.bulkUpdate(
                Collections.emptyList(),
                new ClientDTO(),
                Collections.emptyList(),
                ANALYST,
                SOURCE_FAF
        );

        // Verify nothing was called
        verify(clientsRepository, never()).findClientsByFafIds(any());
        verify(clientsRepository, never()).save(any());
    }

    @Test
    void testBulkUpdate_ExceptionHandling() {
        // Arrange: Simulate an exception in client conversion
        when(clientConverter.convertToDTO(any())).thenThrow(new RuntimeException("Conversion Failed"));

        // Act
        assertDoesNotThrow(() ->
                clientsServiceImpl.bulkUpdate(
                        List.of("faf1"),
                        new ClientDTO(),
                        List.of(new ClientDetailsDTO()),
                        ANALYST,
                        SOURCE_FAF
                )
        );

        // Verify execution did not crash completely
        verify(clientsRepository, times(1)).findClientsByFafIds(any());
        verify(clientsRepository, never()).save(any()); // Save should never be called
    }
}
